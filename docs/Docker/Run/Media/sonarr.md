# Sonarr 电视剧整理

## 准备工作

创建目录

```bash
mkdir -p /opt/sonarr/config
```

## 启动容器

/mnt/down 为挂载的媒体文件位置

```bash
docker run -d \
--name=sonarr \
-e PUID=0 \
-e PGID=0 \
-e TZ=Asia/Shanghai \
-p 8989:8989 \
-v /opt/sonarr/:/config \
-v /mnt/down:/downloads \
--restart always \
lscr.io/linuxserver/sonarr:latest
```
