---
title: Ubuntu 常用设置
description: 
published: true
date: 2022-11-25T14:01:23.229Z
tags: ubuntu
editor: markdown
dateCreated: 2022-11-04T13:20:38.549Z
---

## 安装 SSHD 服务

```bash
sudo apt install openssh-server
# sudo vim /etc/ssh/sshd_config       # PermitRootLogin yes
sudo systemctl restart sshd
```

## 设置环境变量
* 以anaconda为例
```bash
export PATH=$PATH:/usr/local/anaconda3/bin
```

## 设置时区
* 可以通过首字母快速搜索
```bash
sudo dpkg-reconfigure tzdata
```
## SSH免密登录
* 在客户机生产密钥对 (id_rsa, id_rsa.pub)
```bash
ssh-keygen -t rsa
```
* 将公钥内容添加到服务器机器 (id_rsa.pub)
```bash
cd /root/.ssh/
echo "ssh-rsa *******" > authorized_keys
chmod 600 authorized_keys
# 例
# echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDJXhPHzYyT8pkIIkACZ85KwgTA3/BuFNtj1qbOFvQvUU19Z9SIgZoCYZR+vhGKpLESmj9HnQydfDn6H5lqslsmyis2kXqSYtmYwDGRYERXtg+gLIHItlmJOGmNw5i6EAe24JXjlGZnmxP64TOQieDT/EdiE2g+Wdlg8JsAPGfdc/2gpqNuevRbIYCUJAiPTdXSZvYNVac+CIaxfeRwaED77iMbNX7mMCLGhHQSAbQjW7Tykyr6+fTFN1gc7OyJmMvptOU6dDxn4BL4XooNFVZv5Gl28UdPzdrwVYmFETRjIfkzY//QX9qS99p3d9g/lIITnti6H1RTI0AXS9MagRwRhGH4AwJHWDiUy/UquvnoTVCGJ5TN/mRznnc10qsmjrZXVGOkL5eq5SGYeIbvqvZD+8xj6BsFbyuWICvXnFA/6PpFPq8Fk35l4Aksgr3/09UD08LwDgzjMsSaSrrCdTfLCCYzBvL4xMEVpmlx0lewbNcF9ntuPyiLnIsqeD36VE8= root@Test" > authorized_keys
```
* 注意确保 authorized_keys 文件权限为600
