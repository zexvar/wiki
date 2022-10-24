---
title: Minio 文件存储服务部署
description: 
published: 1
date: 2022-10-24T13:06:10.215Z
tags: docker, minio
editor: markdown
dateCreated: 2022-08-06T14:47:23.521Z
---

### MinIO 临时部署:
* 运行容器
   ```bash
   docker run -d --restart=always --name minio -p 9000:9000 -p 9001:9001 minio/minio server /data --console-address ":9001"
   ```
### MinIO 持久化部署

* 创建目录

  ```bash
  mkdir -p /opt/minio/data
  ```
* 启动容器

  ```bash
  docker run --restart=always\
  -p 9000:9000 -p 9001:9001 --name minio \
  -v /opt/minio/data:/data \
  -e "MINIO_ROOT_USER=minioadmin" \
  -e "MINIO_ROOT_PASSWORD=minioadmin" \
  -d minio/minio  \
  server /data --console-address ":9001"
  ```


