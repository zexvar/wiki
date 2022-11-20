---
title: Docker Alist 聚合云盘部署
description: 
published: true
date: 2022-11-20T12:36:01.836Z
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
      xhofe/alist:main
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
    mkdir -p /opt/alist/storage
    ```
* 启动容器
    ```bash
    docker run -d --restart=always \
      -p 5244:5244 --name="alist" \
      -v /opt/alist/data:/opt/alist/data \
      -v /opt/alist/storage:/opt/alist/storage \
      xhofe/alist:main
    ```
* 查看密码
    ```bash
    docker logs alist
    ## Successfully created the admin user and the initial password is: FwZ72nvw ##
    ```