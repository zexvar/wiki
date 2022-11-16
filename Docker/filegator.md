---
title: Docker filegator 文件服务器部署
description: 
published: true
date: 2022-11-16T15:28:48.585Z
tags: docker, filegator
editor: markdown
dateCreated: 2022-11-16T15:28:48.585Z
---

## 创建目录并设置权限
* 文件和文件夹权限拥有者必须为 www-data 
* uid=33 gid=33
```bash
mkdir -p /opt/filegator/data
chown -R 33:33 /opt/filegator/data 
```

## 创建容器
```bash
docker run -d --restart=always \
-p 8000:80 --name filegator \
-v /opt/filegator/data:/var/www/filegator/repository \
filegator/filegator
```


## 修改设置
* 从容器拷贝设置文件到宿主机
```bash
docker cp filegator:/var/www/filegator/configuration.php configuration.php
```
* 修改上传文件大小限制
```bash
'upload_max_size' => 10 * 1024 * 1024 * 1024, // 10GB
```
* 将修改后的配置文件拷贝回容器
```bash
docker cp configuration.php filegator:/var/www/filegator/configuration.php 
```
* 重启容器完成设置
```bash
docker restart filegator
```