---
title: ESXI 网卡驱动安装
---

## 网卡驱动下载

此 r8125 驱动仅支持 ESXI 6.7 版本

[下载链接](https://github.com/realganfan/r8125-esxi/releases/)

## 上传驱动

通过`scp`命令将 VIB 驱动文件上传至 ESXI 服务器的 `/tmp` 目录

## 安装驱动

使用 esxcli 命令

```bash
esxcli software vib install -v /tmp/Realtek_bootbank_net-r8125_9.007.01-1.vib
```

## 重启主机

检查网卡状态
