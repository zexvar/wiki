---
title: Radarr 电影库整理
description: 
published: true
date: 2023-05-20T08:53:33.470Z
tags: docker
editor: markdown
dateCreated: 2023-05-20T08:53:33.470Z
---

## 创建配置目录
`mkdir -p /opt/radarr/config`

## 启动容器
/mnt/down 挂载的媒体文件位置
```
docker run -d \
--name=radarr \
-e PUID=0 \
-e PGID=0 \
-e TZ=Asia/Shanghai \
-p 7878:7878 \
-v /opt/radarr/config:/config \
-v /mnt/down:/downloads \
--restart always \
lscr.io/linuxserver/radarr:latest
```
