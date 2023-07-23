# Radarr 电影库整理

## 准备工作

创建目录

```bash
mkdir -p /opt/radarr/config
```

## 启动容器

/mnt/down 为挂载的媒体文件位置

```bash
docker run -d \
--name=radarr \
-e PUID=0 \
-e PGID=0 \
-e TZ=Asia/Shanghai \
-p 7878:7878 \
-v /opt/radarr/:/config \
-v /mnt/down:/downloads \
--restart always \
lscr.io/linuxserver/radarr:latest
```
