---
title: Watchtower 更新容器
---

## 更新所有容器

```bash
docker run --rm \
-v /var/run/docker.sock:/var/run/docker.sock \
containrrr/watchtower \
--run-once -c
```

- -c 升级后删除旧的 docker 镜像

## 指定容器名进行更新

```bash
docker run --rm \
-v /var/run/docker.sock:/var/run/docker.sock \
containrrr/watchtower \
--run-once -c container_name
```

- -c 升级后删除旧的 docker 镜像
- container_name 为需要被升级的容器名
