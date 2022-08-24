---
title: Docker升级容器
description: 通过watchtower更新容器使用镜像版本
published: 1
date: 2022-08-24T19:30:59.559Z
tags: docker
editor: markdown
dateCreated: 2022-08-07T14:47:05.026Z
---

### Docker升级容器

1. 通过watchtower升级container:

   ```bash
    docker run --rm \
    -v /var/run/docker.sock:/var/run/docker.sock \
    containrrr/watchtower \
    --run-once container_name
   ```
   
   * container_name 为需要被升级的容器名
