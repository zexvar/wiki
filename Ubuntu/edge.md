---
title: Ubuntu 命令行安装Edge浏览器
description: 
published: true
date: 2023-01-24T17:02:53.875Z
tags: ubuntu
editor: markdown
dateCreated: 2023-01-24T17:02:53.875Z
---


## 安装所需的软件包
```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common wget -y
```

## 添加GPG和官方源
```bash
# GPG
sudo wget -O- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | sudo tee /usr/share/keyrings/microsoft-edge.gpg
# 官方源
echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/microsoft-edge.gpg] https://packages.microsoft.com/repos/edge stable main' | sudo tee /etc/apt/sources.list.d/microsoft-edge.list
```

## 安装edge
```
sudo apt update
sudo apt install microsoft-edge-stable
```

## 以root用户身份使用edge

vim /usr/share/applications/microsoft-edge.desktop

将其中的：

Exec=/usr/bin/microsoft-edge-stable %U
Exec=/usr/bin/microsoft-edge-stable
Exec=/usr/bin/microsoft-edge-stable --inprivate
替换为：

Exec=/usr/bin/microsoft-edge-stable %U --no-sandbox
Exec=/usr/bin/microsoft-edge-stable --no-sandbox
Exec=/usr/bin/microsoft-edge-stable --inprivate --no-sandbox
