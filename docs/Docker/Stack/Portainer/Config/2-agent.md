# Agent only

## 准备工作

创建配置文件

```yaml title='portainer-stack.yml'
version: "3.9"

services:
  agent:
    image: portainer/agent
    networks:
      - agent_network
    ports:
      - 9001:9001
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /var/lib/docker/volumes:/var/lib/docker/volumes
    environment:
      - AGENT_SECRET=${AGENT_SECRET}
    deploy:
      mode: global
      placement:
        constraints: [node.platform.os == linux]

networks:
  agent_network:
      driver: overlay
      attachable: true
```

## 部署运行

设置 `AGENT_SECRET` 变量 : 当 Portainer 和 Agent 此变量值不同时拒绝连接

加入 `proxy` 网络 : 为使用 Traefik 代理 Portainer 做准备

```bash
export AGENT_SECRET=123456
docker network create --driver overlay proxy --attachable
docker stack deploy -c portainer-stack.yml portainer
```
