---
title: Filebrowser 轻量网盘列表工具
description: 
published: true
date: 2023-05-08T03:15:17.029Z
tags: cloud, docker
editor: markdown
dateCreated: 2023-02-13T15:40:16.204Z
---

## 创建目录并设置权限
```bash
mkdir -p /opt/filebrowser
touch /opt/filebrowser/database.db
```

## 创建容器
* mnt 挂载远程文件夹
```bash
docker run -d --name=filebrowser \
-p 8000:80 \
-v /mnt/file:/srv \
-v /opt/filebrowser/database.db:/database.db \
--restart=always \
filebrowser/filebrowser
```
* 默认 `用户名/密码` 为 `admin/admin`

## 设置文件
* 默认设置文件在容器内路径为 `/.filebrowser.json`
* 默认设置内容
```json
{
  "port": 80,
  "baseURL": "",
  "address": "",
  "log": "stdout",
  "database": "/database.db",
  "root": "/srv"
}
```