---
title: Ubuntu samba 服务端配置
description: 
published: 1
date: 2022-09-02T12:57:21.021Z
tags: 
editor: markdown
dateCreated: 2022-09-02T12:57:21.021Z
---

## samba 服务端配置
* 安装samba
```bash
sudo apt-get install samba
```

* 创建共享文件夹并设置权限
```bash
sudo mkdir /share
sudo chmod -R 777 /share
```

* 设置samba用户,以admin为例
```bash
useradd admin
sudo smbpasswd -a admin
```

* 修改samba配置文件
```bash
sudo vi /etc/samba/smb.conf
```

```ini
[samba]
comment = Share Directories
path = /share
public = yes
writable = yes
browseable = yes
create mask = 777
directory mask = 777
```

* 服务启动
```bash
service smbd start      #启动
service smbd stop       #停止
service smbd restart    #重启
```