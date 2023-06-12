---
title: PostgreSQL 数据库部署
description: 
published: true
date: 2022-12-04T09:40:19.201Z
tags: docker, postgres
editor: markdown
dateCreated: 2022-12-04T09:39:51.594Z
---

### PostgreSQL 临时部署
* 运行容器
   ```bash
    docker run -d --restart=always --name postgres -p 5432:5432 -e POSTGRES_PASSWORD=123456 postgres
   ```
### PostgreSQL 持久化部署

* 创建目录

  ```bash
  mkdir -p /opt/postgres/data
  ```
* 启动容器

  ```bash
    docker run -d --restart=always --name postgres \
    -p 5432:5432 \
    -e POSTGRES_PASSWORD=123456 \
    -v /opt/postgres/data:/var/lib/postgresql/data \
    postgres
  ```