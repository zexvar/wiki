---
title: Docker部署Mysql服务器
description: 
published: 1
date: 2022-07-15T14:23:18.184Z
tags: docker, mysql
editor: markdown
dateCreated: 2022-07-15T14:23:16.190Z
---

### Mysql
1. 临时部署: 
    ```bash
    docker run --restart=always --privileged=true  -p 3306:3306 --name mysql   -e MYSQL_ROOT_PASSWORD=123456 -d mysql
    ```

2. 持久化部署
* 创建目录
    ```bash
    mkdir -p /opt/mysql/logs/
    mkdir -p /opt/mysql/data/
    ```
* 创建my.cnf配置文件 添加以下内容:
vim /opt/mysql/my.cnf

    ```ini
    [mysqld]
    user=mysql
    character-set-server=utf8
    default_authentication_plugin=mysql_native_password
    secure_file_priv=/var/lib/mysql
    expire_logs_days=7
    sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION
    max_connections=1000

    [client]
    default-character-set=utf8

    [mysql]
    default-character-set=utf8
    ```
* 启动容器
    ```bash
    docker run --restart=always --privileged=true  \
    -p 3306:3306 --name mysql \
    -v /opt/mysql/data:/var/lib/mysql \
    -v /opt/mysql/logs:/var/log/mysql \
    -v /opt/mysql/my.cnf:/etc/mysql/my.cnf \
    -e MYSQL_ROOT_PASSWORD=123456 -d mysql
    ```
