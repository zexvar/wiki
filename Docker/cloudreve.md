---
title: Docker Cloudreve 云盘部署
description: 
published: true
date: 2022-11-20T12:38:12.152Z
tags: cloud, docker
editor: markdown
dateCreated: 2022-11-04T13:20:18.998Z
---

## 创建目录
```bash
mkdir -p /opt/cloudreve/uploads
mkdir -p /opt/cloudreve/avatar
```

## 设置mysql数据库作为存储

* 创建配置文件
```bash
vim /opt/cloudreve/conf.ini
```

* 添加以下内容
```ini
[Database]
Type = mysql
Port = 3306
User = root
Password = 123456
Host = 127.0.0.1
Name = cloudreve
TablePrefix = cd
Charset = utf8
```

## 启动容器
```bash
docker run -d --restart=always --privileged=true \
-p 80:5212 --name cloudreve \
--mount type=bind,source=/opt/cloudreve/conf.ini,target=/cloudreve/conf.ini \
-v /opt/cloudreve/uploads:/cloudreve/uploads \
-v /opt/cloudreve/avatar:/cloudreve/avatar \
cloudreve/cloudreve:latest
```