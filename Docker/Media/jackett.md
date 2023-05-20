---
title: Jackett 索引器
description: 
published: true
date: 2023-05-20T08:57:00.199Z
tags: docker
editor: markdown
dateCreated: 2023-05-20T08:57:00.199Z
---

## 启动容器

使用linuxserver提供的镜像

```bash
docker run -d \
--name=jackett \
-e AUTO_UPDATE=true \
-p 9117:9117 \
-v /opt/jackett/config:/config \
--restart always \
lscr.io/linuxserver/jackett:latest
```

## 添加索引

点击 [Add indexer] 选取需要的索引
