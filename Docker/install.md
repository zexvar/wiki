---
title: Docker Engine 安装
description: 
published: true
date: 2023-05-30T15:17:15.884Z
tags: docker
editor: markdown
dateCreated: 2023-05-30T15:17:15.884Z
---

## 各发行版架构支持

| Platform | x86_64 / amd64 | arm64 / aarch64 | arm (32-bit) |
| -------- | -------------- | --------------- | ------------ |
| CentOS   | yes            | yes             | -            |
| Debian   | yes            | yes             | yes          |
| Fedora   | yes            | yes             | -            |
| Ubuntu   | yes            | yes             | yes          |
| Binaries | yes            | yes             | yes          |

## 通过脚本快速安装
使用官方脚本
```shell
curl -fsSL https://get.docker.com | sh
```
使用阿里云镜像加速
```shell
curl -fsSL https://get.docker.com | sh -s docker --mirror Aliyun
```
## 手动安装

打开[Docker engine](https://docs.docker.com/engine/install/)的官方安装手册
根据操作系统选择对应的发行版,按照手册完成安装

