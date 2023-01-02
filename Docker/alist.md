---
title: Docker Alist 聚合云盘部署
description: 
published: true
date: 2023-01-02T08:04:09.400Z
tags: cloud, docker
editor: markdown
dateCreated: 2022-11-04T13:20:13.439Z
---

## 无本地存储部署
* 创建目录
    ```bash
    mkdir -p /opt/alist/data
    ```
* 启动容器
    ```bash
    docker run -d --restart=always \
    -p 5244:5244 --name="alist" \
    -v /opt/alist/data:/opt/alist/data \
    xhofe/alist:latest
    ```
* 查看密码
    ```bash
    docker logs alist
    ## Successfully created the admin user and the initial password is: FwZ72nvw ##
    ```
## 本机存储部署
* 创建目录
    ```bash
    mkdir -p /opt/alist/data
    # 此处挂载路径为 /mnt/alist
    ```
* 启动容器
    ```bash
    docker run -d --restart=always \
    -p 5244:5244 --name="alist" \
    -v /opt/alist/data:/opt/alist/data \
    -v /mnt/alist:/opt/alist/storage \
    xhofe/alist:latest
    ```
* 查看密码
    ```bash
    docker logs alist
    ## Successfully created the admin user and the initial password is: FwZ72nvw ##
    ```
## 更换为Mysql数据库
* 停止容器
    ```bash
    docker stop alist
    ```
* 编辑配置文件
    ```bash
    vim /opt/alist/data/config.json
    ```
* 配置正确的数据库地址
    ```json
		"database": {
        "type": "mysql",
        "host": "127.0.0.1",
        "port": 3306,
        "user": "root",
        "password": "123456",
        "name": "alist",
        "db_file": "data/data.db",
        "table_prefix": "x_",
        "ssl_mode": ""
  	}
    ```
* 重新启动容器 
  ```bash
  docker start alist
  ```
	重新启动容器后数据库会自动重新建表 
  
* 迁移旧数据
    1. 使用数据库工具打开 `/opt/alist/data/data.db` 类型为sqlite3
    2. 清除mysql数据库中自动生成的数据
    3. 导入旧数据
    	a. 将sqlite数据库中的数据粘贴到对应表
    	b. 从sqlite导出sql语句,在mysql中执行
    
    
    