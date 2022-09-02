---
title: Docker部署Minio服务
description: 
published: 1
date: 2022-08-06T15:06:42.123Z
tags: docker, minio
editor: markdown
dateCreated: 2022-08-06T14:47:23.521Z
---

### MinIO

1. 临时部署:

   ```bash
   docker run -d --restart=always --name minio -p 9000:9000  -p 9001:9001 minio/minio server /data --console-address ":9001"
   ```
2. 持久化部署

* 创建目录

  ```bash
  mkdir -p /opt/minio/data
  ```
* 启动容器

  ```bash
  docker run --restart=always --privileged=true  \
  -p 9000:9000 -p 9001:9001 --name minio \
  -v /opt/minio/data:/data \
  -e "MINIO_ROOT_USER=minioadmin" \
  -e "MINIO_ROOT_PASSWORD=minioadmin" \
  -d minio/minio  \
  server /data --console-address ":9001"
  ```


