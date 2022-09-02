---
title: Ubuntu 常用设置
description: 
published: 1
date: 2022-09-02T12:51:59.995Z
tags: ubuntu
editor: markdown
dateCreated: 2022-09-02T12:51:59.995Z
---

## 安装 sshd 服务

```python
sudo apt install openssh-server
sudo vim /etc/ssh/sshd_config       # PermitRootLogin yes
sudo systemctl restart sshd
```

## 设置环境变量
* 以anaconda为例
```shell
export PATH=$PATH:/usr/local/anaconda3/bin
```

## 设置时区
* 可以通过首字母快速搜索
```shell
sudo dpkg-reconfigure tzdata
```
