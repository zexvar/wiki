# Docker Update 更新容器

## Docker run

### 更新所有容器并删除旧的镜像

```bash
docker run --rm \
-v /var/run/docker.sock:/var/run/docker.sock \
containrrr/watchtower \
--run-once -c
```

### 根据容器名进行更新

```bash
docker run --rm \
-v /var/run/docker.sock:/var/run/docker.sock \
containrrr/watchtower \
--run-once -c container_name
```

## Docker compose

修改 `docker-compose.yml` 镜像版本

```bash
docker compose pull
docker compose down
docker compose up -d
# clear old images
docker image prune
```

## Docker stack

修改 `stack.yml` 镜像版本

```bash
docker stack deploy -c stack.yml stack
```
