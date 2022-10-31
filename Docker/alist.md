---
title: Docker alist云盘部署
description: 
published: 1
date: 2022-10-21T18:19:18.277Z
tags: cloud, docker
editor: markdown
dateCreated: 2022-10-21T18:19:12.753Z
---

### Alist
1. 持久化部署
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