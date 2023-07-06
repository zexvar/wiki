# Cloudreve 云盘

## 准备工作

创建目录

```bash
mkdir -p /opt/cloudreve/uploads
mkdir -p /opt/cloudreve/avatar
```

创建配置文件

```ini title='/opt/cloudreve/conf.ini'
[Database]
Type = mysql
Port = 3306
User = root
Password = 123456
Host = 127.0.0.1
Name = cloudreve
TablePrefix = cd
Charset = utf8
```

## 启动容器

```bash
docker run -d --restart=always --privileged=true \
-p 5212:5212 --name cloudreve \
--mount type=bind,source=/opt/cloudreve/conf.ini,target=/cloudreve/conf.ini \
-v /opt/cloudreve/uploads:/cloudreve/uploads \
-v /opt/cloudreve/avatar:/cloudreve/avatar \
cloudreve/cloudreve:latest
```
