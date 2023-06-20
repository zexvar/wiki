# AX9K 刷入 OpenWrt

## 解锁 SSH

通过开发版 docker 挂载宿主机路径开启 SSH
固化 SSH 后 通过 Telnet 开启 SSH,并修改 root 密码为 admin：

```bash
sed -i 's/channel=.*/channel="debug"/g' /etc/init.d/dropbear
/etc/init.d/dropbear start
echo -e 'admin\nadmin' | passwd root
```

## 无线网络问题

5.2G 网络无法连接

[解决方案](https://openwrt.org/toh/xiaomi/ax9000#potential_issueslimitations)

## 确定当前使用分区

```bash
nvram get flag_last_success
```

| 结果 | 当前使用分区 | 将要刷入分区 |
| ---- | ------------ | ------------ |
| 0    | /dev/mtd21   | /dev/mtd22   |
| 1    | /dev/mtd22   | /dev/mtd21   |

可通过以下命令切换分区

```bash
nvram set flag_last_success=0
nvram set flag_boot_rootfs=0
nvram commit
reboot
```

## 刷入底包

通过 SSH 将底包上传到`/tmp`目录

当前分区为 flag 为 0

```bash
ubiformat /dev/mtd22 -y -f /tmp/openwrt-xxxx-factory.ubi
nvram set flag_last_success=1
nvram set flag_boot_rootfs=1
nvram commit
reboot
```

当前分区为 flag 为 1

```bash
ubiformat /dev/mtd21 -y -f /tmp/openwrt-xxxx-factory.ubi
nvram set flag_last_success=0
nvram set flag_boot_rootfs=0
nvram commit
reboot
```

## 升级系统

路由器重启后通过 Openwrt 升级界面刷入最新系统

## 切换为原系统

```bash
fw_setenv flag_last_success 0
fw_setenv flag_boot_rootfs 0
reboot
```
