# Gateway 网关服务

## 服务组成

- `nginx` 负责反向代理作为网管入口
- `acme` 负责生成和更新 SSL 证书

## 配置文件

```yml title='docker-compose.yml'
version: "3.9"
services:
  nginx:
    image: nginx:latest
    container_name: nginx
    network_mode: host
    volumes:
      - /etc/nginx/nginx.conf:/etc/nginx/nginx.conf
      - /etc/nginx/conf.d:/etc/nginx/conf.d
      - /etc/nginx/ssl:/etc/nginx/ssl
      - /etc/hosts:/etc/hosts
    restart: always

  acme:
    image: neilpang/acme.sh:latest
    container_name: acme
    network_mode: host
    volumes:
      - /etc/acme:/acme.sh
      - /etc/nginx/ssl/:/ssl
    environment:
      - CF_Token=******
      - CF_Account_ID=******
    restart: always
    command: daemon
```

## 启动服务

后台运行 `docker compose up -d`

## ACME 配置

```shell
# 生成证书
docker exec acme --set-default-ca --server letsencrypt --issue --dns dns_cf -d *.abc.com

# 安装证书
docker exec acme --install-cert -d *.abc.com --key-file /ssl/key.pem --fullchain-file /ssl/cert.pem
```

定时更新证书 `0 0 * * * docker exec acme --cron`
