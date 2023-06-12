---
title: Ubuntu 配置静态ip
description: 
published: 1
date: 2022-09-02T07:45:41.974Z
tags: 
editor: markdown
dateCreated: 2022-08-28T11:26:07.879Z
---

## Ubuntu 20.04
- 编辑网卡配置文件
	vim /etc/netplan/*.yaml
```yaml
network:
  ethernets:
    ens33:
      dhcp4: no
      addresses: [192.168.0.100/16]
      optional: true
      gateway4: 192.168.0.1
      nameservers:
        addresses: [8.8.8.8]
  version: 2
```
- 使配置文件生效
	sudo netplan apply


## Ubuntu 22.04
- 在Ubuntu 22.04中routes代替了gateway
- 编辑网卡配置文件
	vim /etc/netplan/*.yaml
```yaml
network:
  ethernets:
    ens160:
      addresses:
      - 192.168.0.100/16
      dhcp6: true
      routes:
        - to: default
          via: 192.168.0.1
      nameservers:
        addresses:
        - 8.8.8.8
        search: []
  version: 2
```
- 使配置文件生效
	sudo netplan apply
