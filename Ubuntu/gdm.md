---
title: Ubuntu Gdm 设置root用户自动登录
description: 
published: true
date: 2022-12-09T14:01:51.892Z
tags: 
editor: markdown
dateCreated: 2022-12-09T14:01:51.892Z
---

### 修改gdm设置
修改下列两个文件
* sudo vim /etc/pam.d/gdm-password 
* sudo vim /etc/pam.d/gdm-autologin
```
# 注释下行
# auth required pam_succeed_if.so user ！= root quiet_success
```

### 修改/root/.profile文件
sudo vim /root/.profile

```
# 注释下行
# mesg n 2 > /dev/null || true
# 添加
tty -s && mesg m || true
```

### 设置自动登录
sudo vim /etc/gdm3/custom.conf

```ini
AutomaticLoginEnable=True 
AutomaticLogin=root
```