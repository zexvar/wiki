---
title: Redis 数据库
---

## 快速部署

无数据持久化

```bash
docker run -itd --restart=always --name redis -p 6379:6379 redis --requirepass 123456
```

## 准备工作

创建目录

```bash
mkdir -p /opt/redis/conf
mkdir -p /opt/redis/data/
```

创建配置文件

```ini title='/opt/redis/conf/redis.conf '
# 允许所有ip访问
bind 0.0.0.0
# 开启混合持久化
aof-use-rdb-preamble yes
```

## 运行容器

启动容器

```bash
docker run --restart=always --privileged=true  \
-p 6379:6379 --name redis \
-v /opt/redis/data:/data \
-v /opt/redis/conf/redis.conf:/etc/redis/redis.conf \
-d redis redis-server /etc/redis/redis.conf \
--requirepass 123456
```
