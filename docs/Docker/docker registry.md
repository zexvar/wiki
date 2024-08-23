# Docker Registry 镜像搭建

## 准备工作

创建 registry 所需配置文件

```yml title='data/registry/config.yml'
version: 0.1
log:
  level: error

storage:
  delete:
    enabled: true
  filesystem:
    rootdirectory: /var/lib/registry
  maintenance:
    uploadpurging:
      enabled: false

http:
  addr: :5000

proxy:
  remoteurl: https://registry-1.docker.io
```

## 启动容器

```yml title='docker-compose.yml'
services:
  registry:
    image: registry
    container_name: registry
    ports:
      - 5000:5000
    volumes:
      - ./data/registry/config.yml:/etc/docker/registry/config.yml
      - ./data/registry/data:/var/lib/registry
    restart: always
```

## 使用镜像

```json title='/etc/docker/daemon.json'
{
  "registry-mirrors": ["http://127.0.0.1:5000"]
}
```
