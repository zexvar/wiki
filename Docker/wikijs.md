---
title: Docker Wikijs 个人维基知识库部署
description: 
published: true
date: 2022-12-19T05:45:58.794Z
tags: docker
editor: markdown
dateCreated: 2022-12-19T05:43:51.389Z
---

## 部署准备
* 创建目录
```bash
mkdir /opt/wikijs
mkdir /opt/wikijs/config
mkdir /opt/wikijs/data
```

## 数据库参数
| 参数    | 值                                                           |
| ------- | ------------------------------------------------------------ |
| DB_TYPE | Type of database (mysql, postgres, mariadb, mssql or sqlite) |
| DB_HOST | Hostname or IP of the database                               |
| DB_PORT | Port of the database                                         |
| DB_USER | Username to connect to the database                          |
| DB_PASS | Password to connect to the database                          |
| DB_NAME | Database name                                                |

## 使用mysql数据库
```bash
docker run -d \
--name=wikijs \
-e PUID=0 \
-e PGID=0 \
-e TZ=Asia/Shanghai \
-p 3000:3000 \
-v /opt/wikijs/config:/config \
-v /opt/wikijs/data:/data \
--restart always \
-e "DB_TYPE=mysql" \
-e "DB_HOST=127.0.0.1" \
-e "DB_PORT=3306" \
-e "DB_USER=root" \
-e "DB_PASS=123456" \
-e "DB_NAME=wikijs" \
lscr.io/linuxserver/wikijs:latest
```

## 使用内置sqlite数据库
```bash
docker run -d \
--name=wikijs \
-e PUID=0 \
-e PGID=0 \
-e TZ=Asia/Shanghai \
-p 3000:3000 \
-v /opt/wikijs/config:/config \
-v /opt/wikijs/data:/data \
--restart always \
lscr.io/linuxserver/wikijs:latest
```

