---
title: Alist 聚合云盘
description: 
published: true
date: 2023-05-08T03:12:12.835Z
tags: cloud, docker
editor: markdown
dateCreated: 2022-11-04T13:20:13.439Z
---
## 准备工作
创建目录
```bash
mkdir -p /opt/alist/data
```

## 运行容器
启动容器
```bash
docker run -d --restart=always \
-p 5244:5244 --name="alist" \
-v /opt/alist/data:/opt/alist/data \
xhofe/alist:latest
```

## 初始密码
查看随机生成的初始密码
```bash
docker logs alist
## Successfully created the admin user and the initial password is: FwZ72nvw ##
```

## 其他数据库
默认数据库为sqlite 切换成MySQL数据库获取更好的性能

编辑配置文件
```json title='/opt/alist/data/config.json'
"database": {
    "type": "mysql",
    "host": "127.0.0.1",
    "port": 3306,
    "user": "root",
    "password": "123456",
    "name": "alist",
    "db_file": "data/data.db",
    "table_prefix": "x_",
    "ssl_mode": ""
}
```

重新启动容器
```bash
# 重启后数据库后会自动建表 
docker restart alist
```


## 迁移旧数据

1. 使用数据库工具打开 `/opt/alist/data/data.db` 类型为sqlite3
2. 清除mysql数据库中自动生成的数据
3. 从sqlite导出sql语句,在mysql中执行


