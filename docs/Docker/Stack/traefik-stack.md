# Traefik 反向代理服务部署

## 准备工作

创建配置文件

```yaml title='traefik-stack.yml'
version: "3.9"

services:
  traefik:
    image: traefik:latest
    networks:
      - proxy_network
    ports:
      - 80:80
      - 8080:8080
      # - target: 443
      #   published: 443
      #   mode: host
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    command:
      - --accesslog=true
      - --api.insecure=true
      - --metrics.prometheus=true
      - --entrypoints.web.address=:80
      - --providers.docker.network=proxy_network
      - --providers.docker.swarmMode=true
      - --providers.docker.exposedbydefault=false
      - --providers.docker.endpoint=unix:///var/run/docker.sock
    deploy:
      mode: replicated
      replicas: 1
      placement:
        constraints: [node.role == manager]
      labels:
        - traefik.enable=true
        - traefik.http.routers.traefik-auth.entrypoints=web
        - traefik.http.routers.traefik-auth.rule=HostRegexp(`{host:^traefik.*}`)
        - traefik.http.services.traefik-auth.loadbalancer.server.port=8080
        - traefik.http.routers.traefik-auth.middlewares=auth
        - traefik.http.middlewares.auth.basicauth.users=${BASIC_AUTH}
networks:
  proxy_network:
    external: true

```

## 部署运行


生成密码 : `echo $(htpasswd -nB admin)`

!!! info "在yml直接填写 : `echo $(htpasswd -nB admin) | sed -e s/\\$/\\$\\$/g`"

```bash
export BASIC_AUTH=$(htpasswd -nB admin)
docker stack deploy -c traefik-stack.yml traefik
```
