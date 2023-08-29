# Portainer only

## 准备工作

创建配置文件

```yaml title='portainer-stack.yml'
version: "3.9"

services:
  portainer:
    image: portainer/portainer-ce
    networks:
      - proxy
    ports:
      - 9000:9000
    volumes:
      - portainer_data:/data
    environment:
      - AGENT_SECRET=${AGENT_SECRET}
    deploy:
      mode: replicated
      replicas: 1
      placement:
        constraints: [node.role == manager]
      labels:
        - traefik.enable=true
        - traefik.http.routers.portainer.entryPoints=web
        - traefik.http.routers.portainer.rule=HostRegexp(`{host:^portainer.*}`)
        - traefik.http.services.portainer.loadbalancer.server.port=9000

networks:
  proxy:
    external: true

volumes:
  portainer_data:
    driver_opts:
      type: nfs
      o: addr=10.0.0.30,rw,nfsvers=4
      device: :/nfs/volumes-dev/portainer_data
```

## 部署运行

设置 `AGENT_SECRET` 变量 : 当 Portainer 和 Agent 此变量值不同时拒绝连接

加入 `proxy` 网络 : 为使用 Traefik 代理 Portainer 做准备

```bash
export AGENT_SECRET=123456
docker network create --driver overlay proxy --attachable
docker stack deploy -c portainer-stack.yml portainer
```
