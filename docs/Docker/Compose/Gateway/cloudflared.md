# Cloudflared 内网穿透

## 服务作用

利用 Cloudflared Tunnels 暴露内网服务
通过 Cloudflare Zero Trust Warp 组网

## 配置文件

```yml
services:
  cloudflared:
    container_name: cloudflared
    image: cloudflare/cloudflared
    network_mode: host
    command: tunnel --no-autoupdate --edge-ip-version 4 run --protocol http2 --token  ******
    restart: always
```

## 注意事项

- 默认使用 `quic` 协议通信 运营商对 `quic` 协议存在阻断
- 通过设置 `--protocol http2` 参数 使用 `http2` 协议提高稳定性

## 前置代理

通过 NGINX 增加前置代替提升国内访问速度

`*.aaa.com -> *.bbb.com -> CF -> HOST`

```
map $http_upgrade $connection_upgrade {
    default upgrade;
    '' close;
}

server {
    listen 80;
    server_name ~^(?<subdomain>.+).aaa.com$;

    set $target_host $subdomain.bbb.com

    #sendfile on;
    tcp_nopush on;
    tcp_nodelay on;
    client_max_body_size 1G;

    #proxy_cache off;
    proxy_buffering off;
    proxy_http_version 1.1;
    proxy_request_buffering off;

    proxy_set_header Accept-Encoding "";
    proxy_set_header Range $http_range;
    proxy_set_header If-Range $http_if_range;

    keepalive_timeout 300s;
    keepalive_requests 100;

    resolver 1.1.1.1 8.8.8.8 valid=10s;

    location / {
        proxy_set_header Host $target_host;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection $connection_upgrade;

        proxy_ssl_name $target_host;
        proxy_ssl_server_name on;

        proxy_pass https://$target_host;
        proxy_redirect http://$target_host/ https://$host/;
        proxy_redirect https://$target_host/ https://$host/;
    }
}
```
