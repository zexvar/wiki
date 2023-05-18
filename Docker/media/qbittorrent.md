---
title: Qbittorrent 磁力种子下载工具
description: 
published: true
date: 2023-05-18T02:11:13.942Z
tags: docker
editor: markdown
dateCreated: 2023-05-18T01:57:14.270Z
---

## 创建配置目录
`mkdir -p /opt/qbittorrent/config`

## 直接暴露端口部署
/mnt/down 为宿主机下载的文件保存位置
```
docker run -d \
--name=qbittorrent \
-e PUID=0 \
-e PGID=0 \
-e WEBUI_PORT=8080 \
-p 8080:8080 \
-p 6881:6881 \
-p 6881:6881/udp \
-v /opt/qbittorrent/config:/config \
-v /mnt/down:/downloads \
--restart always \
lscr.io/linuxserver/qbittorrent:latest
```

## 使用宿主机网络部署
通过此方式可以直接支持IPV6上传与下载
```
docker run -d \
--name=qbittorrent \
--network=host \
-e PUID=0 \
-e PGID=0 \
-e TZ=Asian/Shanghai \
-e WEBUI_PORT=8080 \
-v /opt/qbittorrent/config:/config \
-v /mnt/down:/downloads \
--restart=always \
lscr.io/linuxserver/qbittorrent:latest
```