---
title: Docker Frp 内网穿透
description: 
published: true
date: 2022-12-05T13:17:12.116Z
tags: docker, frp
editor: markdown
dateCreated: 2022-11-04T13:20:21.739Z
---

## 部署frp服务端

* 创建frps.ini配置文件

    ```bash
    mkdir -p /opt/frp
    vim /opt/frp/frps.ini
    ```

* 文件内容如下

    ```ini
    [common]
    bind_addr = 0.0.0.0
    bind_port = 7000
    vhost_http_port = 80
    vhost_https_port = 443
    #客户端秘钥
    token = (password)
    dashboard_port = 7500
    dashboard_user = admin
    dashboard_pwd = (password)
    ```

* 运行容器

    ```bash
    docker run --restart=always --network host -d -v /opt/frp/frps.ini:/etc/frp/frps.ini --name frps snowdreamtech/frps
    ```

## 部署frp客户端

* 创建frpc.ini配置文件

    ```bash
    mkdir -p /op/frp
    vim /opt/frp/frpc.ini
    ```

* 文件内容如下

    ```ini
    [common]
    server_addr = (frp server ip)
    server_port = 7000
    token = (password)

    [http]
    type = http
    local_port = 80
    local_ip = 127.0.0.1
    custom_domains = *

    [https]
    type = https
    local_port = 443
    local_ip = 127.0.0.1
    custom_domains = *
    ```

* 运行容器

    ```bash
    docker run --restart=always --network host -d -v /opt/frp/frpc.ini:/etc/frp/frpc.ini --name frpc snowdreamtech/frpc
    ```

### 查看服务状态

* 进入frp控制台
    访问 frp 服务端地址 + 端口号7500
* 输入密码后在 HTTP 和 HTTPS 目录中查看客户端状态