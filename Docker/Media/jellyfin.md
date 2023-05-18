---
title: Jellyfin 影音服务器
description: 
published: true
date: 2023-05-18T02:10:49.886Z
tags: docker
editor: markdown
dateCreated: 2023-05-18T02:10:49.886Z
---


## 使用 Nvidia GPU 硬解部署
需要安装 nvidia-docker2
```bash
# 检查是否安装成功
docker run --rm --gpus all nvidia/cuda:11.8.0-base-ubuntu22.04 nvidia-smi
```

创建配置目录
```bash
mkdir -p /opt/alist/data
```

启动容器
```bash
docker run -d \
--name=jellyfin \
-e PGID=0 \
-e PUID=0 \
-p 8096:8096 \
-v /opt/jellyfin/config:/config \
-v /mnt/down/media:/media \
--restart=always \
--runtime=nvidia \
-e NVIDIA_VISIBLE_DEVICES=all \
lscr.io/linuxserver/jellyfin:latest
```
