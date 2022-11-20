---
title: Windows 基本设置优化
description: 
published: true
date: 2022-11-20T13:14:39.742Z
tags: windows
editor: markdown
dateCreated: 2022-11-20T13:14:39.742Z
---

## Win10专业版系统激活

* 管理员身份运行CMD

```bash
# 卸载旧的密钥
slmgr.vbs /upk
# 安装新的专业版密钥
slmgr /ipk W269N-WFGWX-YVC9B-4J6C9-T83GX
# 设置激活服务器
slmgr /skms kms.yuxuan.work
# 激活系统
slmgr /ato
```

## 设置用户默认权限为管理员

1. 打开本地安全策略 (需要专业版系统) 
* WIN + R 键运行 `secpol.msc`

2. 在本地安全策略中设置属性值
```shell
全设置 -> 本地策略 -> 安全选项 -> 用户帐户控制 -> 本地安全设置 -> 已禁用
```

## 设置开发语言环境

* 通过winget包管理器一键配置

```bash
# java8
winget install BellSoft.LibericaJDK.8
# python3.9
winget install Python.Python.3.9
```