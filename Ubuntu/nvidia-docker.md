---
title: Ubuntu 下安装 nvidia-docker
description: 
published: true
date: 2022-12-22T13:50:53.716Z
tags: docker
editor: markdown
dateCreated: 2022-12-22T13:50:53.716Z
---

## 添加 nvidia-docker2 的apt源
```bash
distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
&& curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add - \
&& curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
```

## 通过apt下载
`sudo apt install -y nvidia-docker2`

## 运行测试
`docker run --rm --gpus all nvidia/cuda:11.8.0-base-ubuntu22.04 nvidia-smi`