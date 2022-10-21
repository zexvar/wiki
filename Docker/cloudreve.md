---
title: Docker Cloudreve私人网盘
description: 
published: 1
date: 2022-10-21T18:22:58.970Z
tags: cloud, docker
editor: markdown
dateCreated: 2022-08-26T06:39:47.754Z
---

1. 创建目录
    ```bash
    mkdir -p /opt/cloudreve/uploads
    mkdir -p /opt/cloudreve/avatar
    ```
2. 设置mysql数据库作为存储
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

3. 启动容器
    ```bash
    docker run -d --restart=always --privileged=true \
    -p 80:5212 --name cloudreve \
    --mount type=bind,source=/opt/cloudreve/conf.ini,target=/cloudreve/conf.ini \
    -v /opt/cloudreve/uploads:/cloudreve/uploads \
    -v /opt/cloudreve/avatar:/cloudreve/avatar \
    cloudreve/cloudreve:latest
    ```