---
title: Ubuntu 添加 IPv6 (Tunnel Broker)
description: 
published: true
date: 2022-11-30T06:04:41.384Z
tags: 
editor: markdown
dateCreated: 2022-11-30T06:04:41.384Z
---

## 本文目标
部分云主机仅有IPV4地址,通过 HE Tunnel Broker为其添加IPV6地址.

## 创建隧道
在Tunnel Broker官网注册账号
* [Tunnel Broker 官网](https://tunnelbroker.net/) 

登录账号并创建隧道,点击 `Create Regular Tunnel` 按钮.
输入 VPS 的 `IPV4` 地址并选择合适的节点.

## 登录到VPS并配置网络参数

修改网络配置: `vim /etc/netplan/00-installer-config.yaml`
``` yaml
# This is the network config written by 'subiquity'
network:
  ethernets:
    enp0s3:
      dhcp4: true
  tunnels:
    he-ipv6:
      mode: sit
      remote: 提供的endpoint ipv4地址
      local: 本地内网ip
      addresses: ['提供的address ipv6地址/提供的netmask']
      # addresses: ['2001:xx:xx::x/64']
      gateway6: 提供的gateway ipv6地址
  version: 2
```
应用设置: `netplan apply`
重启VPS: `reboot`

## 测试IPV6是否正常
```bash
root@vps:~# ping 6.ipw.cn
PING 6.ipw.cn(2402:4e00:1013:e500:0:9671:f018:4947 (2402:4e00:1013:e500:0:9671:f018:4947)) 56 data bytes
64 bytes from 2402:4e00:1013:e500:0:9671:f018:4947 (2402:4e00:1013:e500:0:9671:f018:4947): icmp_seq=1 ttl=49 time=370 ms
64 bytes from 2402:4e00:1013:e500:0:9671:f018:4947 (2402:4e00:1013:e500:0:9671:f018:4947): icmp_seq=2 ttl=49 time=373 ms
64 bytes from 2402:4e00:1013:e500:0:9671:f018:4947 (2402:4e00:1013:e500:0:9671:f018:4947): icmp_seq=3 ttl=49 time=386 ms
64 bytes from 2402:4e00:1013:e500:0:9671:f018:4947 (2402:4e00:1013:e500:0:9671:f018:4947): icmp_seq=4 ttl=49 time=391 ms
```
