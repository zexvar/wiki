---
title: MySQL 数据库部署
description: 
published: true
date: 2022-12-15T10:10:22.787Z
tags: docker, mysql
editor: markdown
dateCreated: 2022-11-04T13:20:07.870Z
---

## Docker 临时部署: 
* 拉取容器 `docker pull mysql`
* 运行容器
    ```bash
    docker run --restart=always --privileged=true -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql
    ```

## Docker 持久化部署
* 创建目录
    ```bash
    mkdir -p /opt/mysql/logs/
    mkdir -p /opt/mysql/data/
    ```
* 创建my.cnf配置文件`vim /opt/mysql/my.cnf`  
* 添加以下内容
    ```ini
    [mysqld]
    skip-name-resolve
    default-time-zone='Asia/Shanghai'
    character-set-server=utf8mb4

    [client]
    default-character-set=utf8mb4
 
    ```
* 启动容器
    ```bash
    docker run --restart=always \
    -p 3306:3306 --name mysql \
    -v /opt/mysql/data:/var/lib/mysql \
    -v /opt/mysql/logs:/var/log/mysql \
    -v /opt/mysql/my.cnf:/etc/mysql/my.cnf \
    -e MYSQL_ROOT_PASSWORD=123456 -d mysql
    ```
