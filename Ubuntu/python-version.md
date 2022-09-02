---
title: Ubuntu 默认python3配置
description: 
published: 1
date: 2022-09-02T12:47:29.588Z
tags: ubuntu
editor: markdown
dateCreated: 2022-09-02T12:47:29.588Z
---

## 设置python版本为python3

```shell
sudo update-alternatives --install /usr/bin/python python /usr/bin/python2 100
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 150
```

## 关闭conda base环境

```shell
conda config --set auto_activate_base false
```