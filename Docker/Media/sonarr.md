---
title: Sonarr 电视剧整理
description: 
published: true
date: 2023-05-20T08:54:48.829Z
tags: docker
editor: markdown
dateCreated: 2023-05-20T08:54:07.656Z
---

## 创建配置目录
`mkdir -p /opt/sonarr/config`

## 启动容器
/mnt/down 挂载的媒体文件位置
```
docker run -d \
--name=sonarr \
-e PUID=0 \
-e PGID=0 \
-e TZ=Asia/Shanghai \
-p 8989:8989 \
-v /opt/sonarr/config:/config \
-v /mnt/down:/downloads \
--restart always \
lscr.io/linuxserver/sonarr:latest
```
