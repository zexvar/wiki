# Traefik 网关入口

## 准备工作

创建网络用于 traefik 路由 docker 服务

```shell
docker network create main
```

创建配置文件

```yml title='traefik.yml'
api:
  insecure: true
  dashboard: true

entryPoints:
  web:
    address: ":80"
    forwardedHeaders:
      insecure: true
  websecure:
    address: ":443"
    forwardedHeaders:
      insecure: true
    http:
      tls:
        certResolver: default
        domains:
        - main: "xxx.com"
          sans:
            - "*.xxx.com"

providers:
  docker:
    watch: true
    exposedByDefault: false
    endpoint: unix:///var/run/docker.sock
  file:
    watch: true
    directory: /etc/traefik/config

certificatesResolvers:
  default:
    acme:
      email: ******
      storage: /etc/traefik/acme.json
      dnsChallenge:
        provider: cloudflare
```

## 配置文件

```yml title='docker-compose.yml'
services:
  traefik:
    image: traefik
    container_name: traefik
    networks:
      - main
    ports:
      - target: 80
        published: 80
        protocol: tcp
        mode: host
      - target: 443
        published: 443
        protocol: tcp
        mode: host
    volumes:
      - ./data/traefik:/etc/traefik
      - /var/run/docker.sock:/var/run/docker.sock
    environment:
      - CF_DNS_API_TOKEN=******
      - CF_ZONE_API_TOKEN=******
      - TZ=Asia/Shanghai
    restart: always
```
