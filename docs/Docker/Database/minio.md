---
title: Minio 文件存储服务
---

## 快速部署

无数据持久化

```bash
docker run -d --restart=always --name minio -p 9000:9000 -p 9001:9001 minio/minio server /data --console-address ":9001"
```

## 准备工作

创建目录

```bash
mkdir -p /opt/minio/data
```

## 运行容器

启动容器

```bash
docker run --restart=always\
-p 9000:9000 -p 9001:9001 --name minio \
-v /opt/minio/data:/data \
-e "MINIO_ROOT_USER=minioadmin" \
-e "MINIO_ROOT_PASSWORD=minioadmin" \
-d minio/minio  \
server /data --console-address ":9001"
```
