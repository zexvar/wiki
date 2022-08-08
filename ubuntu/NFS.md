---
title: Ubuntu NFS 服务端和客户端配置
description: 
published: 1
date: 2022-08-08T20:19:33.849Z
tags: ubuntu, nfs
editor: markdown
dateCreated: 2022-08-08T20:19:33.849Z
---

# Ubuntu NFS 服务端和客户端配置
## NFS服务端搭建
### 启动NFS服务
* sudo apt install nfs-kernel-server

* 检查nfs-server是否已经启动：
``` bash
sudo systemctl status nfs-server
sudo systemctl enable nfs-server
sudo systemctl start nfs-server
```
### 创建NFS共享目录
* sudo mkdir -p /nfs

允许所有客户端访问,分配权限：
``` bash
sudo chown nobody:nogroup /nfs
sudo chmod -R 777 /nfs
```
### 编辑exports配置文件

通过编辑/etc/exports配置文件,设置客户端权限

* sudo vim /etc/exports
  - 设置允许访问的客户端ip
    - /nfs 192.168.0.100(rw,sync,no_subtree_check)
    - /nfs 192.168.0.200(rw,sync,no_subtree_check)
  - 设置允许访问的客户端ip段,通过 * 或者 0.0.0.0/x
    - /nfs 192.168.0.*(rw,sync,no_subtree_check)
    - /nfs 192.168.0.0/24(rw,sync,no_subtree_check)

配置文件中的权限解释：
* rw 读写
* sync 文件同时写入硬盘和内存
* no_subtree_check 即使输出目录是一个子目录,不检查其父目录的权限,这样可以提高效率

### export共享目录

使用下面命令将共享文件夹启用并生效：
* sudo exportfs -arv
查看是否可以看到共享目录：
* showmount -e 


## NFS客户端配置

### 安装NFS客户端
``` bash
sudo apt install nfs-common
```
### 挂载NFS共享目录
客户端创建挂载点目录
``` bash
mkdir -p /nfs-clinet
mount 192.168.0.100:/nfs /nfs-clinet
```


