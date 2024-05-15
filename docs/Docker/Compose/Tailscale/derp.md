# Derp 中转节点

原文

> You must use port TCP 80 for HTTP. By default, HTTPS runs on port 443, and STUN runs on 3478. To use other port numbers for HTTPS and STUN, set DERPNode.DERPPort or DERPNode.STUNPort, respectively.

翻译

> 必须将端口 TCP 80 用于 HTTP。默认情况下，HTTPS 在端口 443 上运行，STUN 在 3478 上运行。要将其他端口号用于 HTTPS 和 STUN，请分别设置 DERPNode.DERPPort 或 DERPNode.STUNPort 。

## 准备工作

构建镜像

```dockerfile title='Dockerfile'
FROM golang:alpine AS builder
RUN go install tailscale.com/cmd/derper@main

FROM alpine
WORKDIR /app
ENV DERP_DOMAIN=hostname.com
ENV DERP_VERIFY_CLIENTS=false
COPY --from=builder /go/bin/derper .
CMD ["/app/derper", "-hostname", "$DERP_DOMAIN", "-verify-clients","$DERP_VERIFY_CLIENTS"]
```

生成镜像 `docker build -t derp .`

## 安装 Tailscale

安装 tailscale `curl -fsSL https://tailscale.com/install.sh | sh`

运行`tailscaled`

## 配置文件

```yaml title='docker-compose.yml'
services:
  derp:
    container_name: derp
    network_mode: host
    image: derp
    volumes:
      - /var/run/tailscale/tailscaled.sock:/var/run/tailscale/tailscaled.sock
    environment:
      - DERP_VERIFY_CLIENTS=true
      - DERP_DOMAIN=<DOMAIN_NAME>
    restart: always
```
