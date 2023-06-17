# Filerowser 轻量网盘

## 准备工作

创建目录和数据库

```bash
mkdir -p /opt/filebrowser
touch /opt/filebrowser/database.db
```

## 运行容器

mnt 为挂载的远程文件夹

```bash
docker run -d --name=filebrowser \
-p 8000:80 \
-v /mnt/file:/srv \
-v /opt/filebrowser/database.db:/database.db \
--restart=always \
filebrowser/filebrowser
```

## 默认密码

默认 `用户名/密码` 为 `admin/admin`

## 设置文件

默认设置内容在容器内

```json title='/.filebrowser.json'
{
  "port": 80,
  "baseURL": "",
  "address": "",
  "log": "stdout",
  "database": "/database.db",
  "root": "/srv"
}
```
