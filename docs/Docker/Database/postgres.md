# PostgreSQL 数据库

## 快速部署

无数据持久化

```bash
docker run -d --restart=always --name postgres -p 5432:5432 -e POSTGRES_PASSWORD=123456 postgres
```

## 准备工作

创建目录

```bash
mkdir -p /opt/postgres/data
```

## 运行容器

```bash
docker run -d --restart=always --name postgres \
-p 5432:5432 \
-e POSTGRES_PASSWORD=123456 \
-v /opt/postgres/data:/var/lib/postgresql/data \
postgres
```
