---
title: Ubuntu Samba 服务搭建和使用
description: 
published: 1
date: 2022-10-29T17:43:31.620Z
tags: 
editor: markdown
dateCreated: 2022-09-02T12:57:21.021Z
---

## Samba 服务端配置
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
## Samba 客户端挂载

* 安装客户端
```bash
sudo apt install cifs-utils 
```

* 创建挂载点并挂载
```bash
mkdir /share
mount //xx.xx.xx.xx/share /share -o username=admin,password=123456,uid=0,gid=0
```
* 开机自动挂载 `vim /etc/fstab`
```bash
//xx.xx.xx.xx/share /share/ cifs defaults,username=admin,password=123456,uid=0,gid=0 0 0
```