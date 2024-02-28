# AX3KT SSH 固化

## SN 信息

|     | SN              | PASS     |
| --- | --------------- | -------- |
| AX1 | 49850/F3UW98898 | 5188618f |
| AX2 | 49850/F3UR03568 | b2436fa5 |

### 开启 SSH

- 软固化

```shell
nvram set ssh_en=1
nvram set telnet_en=1
nvram set uart_en=1
nvram set boot_wait=on
nvram commit
sed -i 's/channel=.*/channel="debug"/g' /etc/init.d/dropbear
/etc/init.d/dropbear restart
echo -e 'admin\nadmin' | passwd root
```

- 硬固化

```shell
zz=$(dd if=/dev/zero bs=1 count=2 2>/dev/null) ; printf '\xA5\x5A%c%c' $zz $zz | mtd write - crash
reboot

# 重启后继续
nvram set ssh_en=1
nvram set telnet_en=1
nvram set uart_en=1
nvram set boot_wait=on
nvram commit
bdata set ssh_en=1
bdata set telnet_en=1
bdata set uart_en=1
bdata set boot_wait=on
bdata commit
reboot

# 重启后继续
mtd erase crash
reboot
```

## 硬固化后通过 Telnet 开启 SSH

```shell
sed -i '/flg_ssh=`nvram get ssh_en`/{:loop; N; /\n.*channel=`\/sbin\/uci get \/usr\/share\/xiaoqiang\/xiaoqiang_version.version.CHANNEL`\n.*return 0\n.\*fi/!b loop; d}' /etc/init.d/dropbear
/etc/init.d/dropbear restart
echo -e 'admin\nadmin' | passwd root
```
