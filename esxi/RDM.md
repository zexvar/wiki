---
title: ESXI RDM磁盘直通
description: 
published: 1
date: 2022-08-24T05:13:43.297Z
tags: esxi
editor: markdown
dateCreated: 2022-08-24T05:13:43.297Z
---

# ESXI 设置RDM磁盘直通
* 开启ESXI主机的ssh服务
* ssh连接ESXI主机
* ```bash 
	vmkfstools -z [磁盘名称] [数据存储路径] [磁盘文件名称].vmdk
  ```
* 操作成功后无提示
* 数据存储中出现新的虚拟磁盘