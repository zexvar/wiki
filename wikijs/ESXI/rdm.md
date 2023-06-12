---
title: ESXI RDM磁盘直通
description: 
published: 1
date: 2022-09-02T07:48:18.305Z
tags: esxi
editor: markdown
dateCreated: 2022-08-24T19:45:47.895Z
---

# ESXI 设置RDM磁盘直通
* 开启ESXI主机的ssh服务
* ssh连接ESXI主机
* ```bash 
	vmkfstools -z [磁盘路径] [数据存储路径]/[磁盘文件名称].vmdk 
  # example
  vmkfstools -z /vmfs/devices/disks/t10.ATA_____TOSHIBA_HDWE140_________________________________41J8K86KFBRG /vmfs/volumes/6300a399-8e448fa0-c392-b42e999d1004/HDD_4TB_TSB.vmdk
  ```
* 操作成功后无提示
* 数据存储中出现新的虚拟磁盘