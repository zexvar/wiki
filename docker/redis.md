---
title: Docker部署Redis服务
description: 
published: 1
date: 2022-08-06T15:06:02.017Z
tags: docker, redis
editor: markdown
dateCreated: 2022-08-06T14:09:52.320Z
---

### Redis
1. 临时部署: 
* 通过 `--requirepass` 设置redis密码
  ```bash
  docker run -itd --restart=always --name redis -p 6379:6379 redis --requirepass 123456
  ```
  
2. 持久化部署
* 创建目录
  ```bash
    mkdir -p /opt/redis/conf
    mkdir -p /opt/redis/data/
  ```
* 创建m配置文件 添加以下内容:
    ```bash
    vim /opt/redis/conf/redis.conf 
    ```
    ```ini
    # 允许所有ip访问
    bind 0.0.0.0
    # 开启混合持久化
    aof-use-rdb-preamble yes
    ```

* 启动容器
    ```bash
    docker run --restart=always --privileged=true  \
    -p 6379:6379 --name redis \
    -v /opt/redis/data:/data \
    -v /opt/redis/conf/redis.conf:/etc/redis/redis.conf \
    -d redis redis-server /etc/redis/redis.conf \
    --requirepass 123456 
    ```


