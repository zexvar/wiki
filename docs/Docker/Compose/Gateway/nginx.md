# Nginx 网关入口

## 服务组成

- `nginx` 负责反向代理作为网关入口
- `acme` 负责生成和更新 SSL 证书

## 通过 ACME 环境变量安装证书

通过 ACME 环境变量设置,指定证书安装位置,并在证书更改后自动重启 nginx 服务,确保新证书被 nginx 使用.

```yml title='docker-compose.yml'
version: "3.9"
services:
  nginx:
    image: nginx
    container_name: nginx
    network_mode: host
    labels:
      - "nginx"
    volumes:
      - /etc/nginx/nginx.conf:/etc/nginx/nginx.conf
      - /etc/nginx/conf.d:/etc/nginx/conf.d
      - /etc/nginx/ssl:/etc/nginx/ssl
      - /etc/hosts:/etc/hosts
    restart: always

  acme:
    image: neilpang/acme.sh
    container_name: acme
    environment:
      - CF_Token=******
      - CF_Account_ID=******
      - DEPLOY_DOCKER_CONTAINER_LABEL="nginx"
      - DEPLOY_DOCKER_CONTAINER_RELOAD_CMD="nginx -s reload"
      - DEPLOY_DOCKER_CONTAINER_KEY_FILE=/etc/nginx/ssl/key.pem
      - DEPLOY_DOCKER_CONTAINER_FULLCHAIN_FILE=/etc/nginx/ssl/cert.pem
    volumes:
      - /etc/acme:/acme.sh
      - /var/run/docker.sock:/var/run/docker.sock:ro
    restart: always
    command: daemon
```

## 手动配置服务

```yml title='docker-compose.yml'
version: "3.9"
services:
  nginx:
    image: nginx
    container_name: nginx
    network_mode: host
    volumes:
      - /etc/nginx/nginx.conf:/etc/nginx/nginx.conf
      - /etc/nginx/conf.d:/etc/nginx/conf.d
      - /etc/nginx/ssl:/etc/nginx/ssl
      - /etc/hosts:/etc/hosts
    restart: always

  acme:
    image: neilpang/acme.sh
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

ACME 配置

```shell
# 生成证书
docker exec acme --set-default-ca --server letsencrypt --issue --dns dns_cf -d *.abc.com

# 安装证书
docker exec acme --install-cert -d *.abc.com --key-file /ssl/key.pem --fullchain-file /ssl/cert.pem
```

定时更新证书 `0 0 * * * docker exec acme --cron`
