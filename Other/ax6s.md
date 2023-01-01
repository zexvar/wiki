---
title: AX6S 刷入 OpenWrt
description: 
published: true
date: 2023-01-01T08:28:35.519Z
tags: openwrt
editor: markdown
dateCreated: 2023-01-01T08:28:35.519Z
---

## 解锁SSH
刷入开发板固件开启Telnet
登录管理界面获取SN码
通过SN码计算root密码 -> [官方网址](https://miwifi.dev/ssh)
通过Telnet登录root用户
```bash
nvram set ssh_en=1 & nvram set uart_en=1 & nvram set boot_wait=on & nvram set bootdelay=3 & nvram set flag_try_sys1_failed=0 & nvram set flag_try_sys2_failed=1
nvram set flag_boot_rootfs=0 & nvram set "boot_fw1=run boot_rd_img;bootm"
nvram set flag_boot_success=1 & nvram commit & /etc/init.d/dropbear enable & /etc/init.d/dropbear start
```

## 刷入底包
上传底包到`/tmp`目录
```bash
mtd -r write /tmp/AX6S底包.bin firmware
```

## 升级系统
路由器重启后通过openwrt升级界面刷入最新系统
