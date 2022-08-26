---
title: Docker部署Cloudreve私人网盘
description: 
published: 1
date: 2022-08-26T06:39:47.754Z
tags: docker, cloud
editor: markdown
dateCreated: 2022-08-26T06:39:47.754Z
---

### Cloudreve
1. 持久化部署
* 创建目录
    ```bash
    mkdir -p /opt/cloudreve/uploads
    mkdir -p /opt/cloudreve/avatar
    ```
* 创建配置文件 添加以下内容:
    ```bash
    vim /opt/cloudreve/conf.ini
    ```
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

* 启动容器
    ```bash
    docker run -d --restart=always --privileged=true \
    -p 80:5212 --name cloudreve \
    --mount type=bind,source=/opt/cloudreve/conf.ini,target=/cloudreve/conf.ini \
    -v /opt/cloudreve/uploads:/cloudreve/uploads \
    -v /opt/cloudreve/avatar:/cloudreve/avatar \
    cloudreve/cloudreve:latest
    ```