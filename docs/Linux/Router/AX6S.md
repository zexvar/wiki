# AX6S 刷入 OpenWrt

## 准备工作

1. 刷入开发板固件开启 Telnet
2. 登录管理界面获取 SN 码

## 开启 SSH

通过 SN 码计算 root 密码 -> [官方网址](https://miwifi.dev/ssh)
通过 Telnet 登录 root 用户
通过命令行开启 SSH 服务

```bash
nvram set ssh_en=1 & nvram set uart_en=1 & nvram set boot_wait=on & nvram set bootdelay=3 & nvram set flag_try_sys1_failed=0 & nvram set flag_try_sys2_failed=1
nvram set flag_boot_rootfs=0 & nvram set "boot_fw1=run boot_rd_img;bootm"
nvram set flag_boot_success=1 & nvram commit & /etc/init.d/dropbear enable & /etc/init.d/dropbear start
```

## 刷入底包

上传底包到`/tmp`目录

```bash
mtd -r write /tmp/openwrt.bin firmware
```

## 升级系统

路由器重启后通过 openwrt 升级界面刷入最新系统
