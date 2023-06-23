# Docker Swarm 集群搭建

## 初始化集群

### 初始化管理节点

```shell
docker swarm init \
--default-addr-pool 172.19.0.0/16 \
--task-history-limit 2

docker swarm init \
--default-addr-pool 172.19.0.0/16 \
--task-history-limit 2 \
--advertise-addr 10.0.0.201
```

### 添加集群节点

根据需要向集群继续添加管理节点或工作节点

显示添加管理节点命令 `docker swarm join-token manager`

显示添加工作节点命令 `docker swarm join-token worker`

在管理节点上查看集群状态 `docker node ls`

## 集群服务测试

```shell
docker service create \
--name whoami \
--replicas 1 \
--publish published=8081,target=80 \
traefik/whoami
```

!!! failure "在 ESXI 平台下 VMXNET3 网卡存在通信问题 (E1000e 网卡正常)"

访问集群中任意节点 8081 端口都应能够响应

## 防火墙端口

查看防火墙规则 `ufw status verbose`

- manager 节点
  `ufw allow 9000` &&
  `ufw allow 2377/tcp` &&
  `ufw allow 7946` &&
  `ufw allow 4789/udp`

- worker 节点
  `ufw allow 7946` &&
  `ufw allow 4789/udp`
