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
    command: tunnel --no-autoupdate --edge-ip-version auto --protocol auto run --token ******
    restart: always
```

## 注意事项

- 默认使用 `quic` 协议通信 运营商对 `quic` 协议存在阻断
- 通过设置 `--protocol http2` 参数 使用 `http2` 协议提高稳定性
