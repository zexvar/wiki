---
title: MySQL 数据库
---

## 快速部署
无数据持久化
```bash
docker run --restart=always --privileged=true -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql
```

## 准备工作
创建目录
```bash
mkdir -p /opt/mysql/logs/
mkdir -p /opt/mysql/data/
```

创建my.cnf配置文件
```ini title='/opt/mysql/my.cnf'
[mysqld]
skip-name-resolve
default-time-zone='Asia/Shanghai'
character-set-server=utf8mb4

[client]
default-character-set=utf8mb4
```

## 运行容器
启动容器
```bash
docker run --restart=always \
-p 3306:3306 --name mysql \
-v /opt/mysql/data:/var/lib/mysql \
-v /opt/mysql/logs:/var/log/mysql \
-v /opt/mysql/my.cnf:/etc/mysql/my.cnf \
-e MYSQL_ROOT_PASSWORD=123456 -d mysql
```
