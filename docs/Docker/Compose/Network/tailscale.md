# Tailscale 组网

> Tailscale makes creating software-defined networks easy: securely connecting users, services, and devices.

官网链接 [Tailscale](https://www.tailscale.com/)

直接安装 `curl -fsSL https://tailscale.com/install.sh | sh`

## Tailscale

### 准备工作

在控制台生成 Auth key 用于身份验证

### 配置文件

```yml title='docker-compose.yml'
services:
  tailscale:
    image: tailscale/tailscale
    container_name: tailscale
    network_mode: host
    cap_add:
      - NET_ADMIN
      - SYS_ADMIN
    volumes:
      - ./data/tailscale:/var/lib/tailscale
      - /dev/net/tun:/dev/net/tun
    environment:
      - TS_USERSPACE=false
      - TS_STATE_DIR=/var/lib/tailscale
      - TS_AUTHKEY=<AUTH_KEY>
    restart: always
```

## Derp

> You must use port TCP 80 for HTTP. By default, HTTPS runs on port 443, and STUN runs on 3478. To use other port numbers for HTTPS and STUN, set DERPNode.DERPPort or DERPNode.STUNPort, respectively.

### 准备工作

构建镜像

```dockerfile title='Dockerfile'
FROM golang:alpine AS builder
RUN go install tailscale.com/cmd/derper@main

FROM alpine
COPY --from=builder /go/bin/derper /usr/bin/derper
ENTRYPOINT ["derper"]
```

生成镜像 `docker build -t derp .`

### 配置文件

```yml title='docker-compose.yml'
services:
  derp:
    image: derp
    container_name: derp
    network_mode: host
    volumes:
      - /var/run/tailscale/tailscaled.sock:/var/run/tailscale/tailscaled.sock
    command: "--hostname=<DOMAIN_NAME> --verify-clients"
    restart: always
```
