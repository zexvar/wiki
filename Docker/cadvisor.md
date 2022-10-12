---
title: Docker部署cadvisor监控容器服务
description: 
published: 1
date: 2022-10-12T04:14:27.664Z
tags: cadvisor, docker
editor: markdown
dateCreated: 2022-10-12T04:10:42.036Z
---

### Cadvisor

1. 部署:
* docker hub 上的镜像已经不再更新
* google提供的镜像国内无法访问

   ```bash
    docker run \
      --volume=/:/rootfs:ro \
      --volume=/var/run:/var/run:ro \
      --volume=/sys:/sys:ro \
      --volume=/var/lib/docker/:/var/lib/docker:ro \
      --volume=/dev/disk/:/dev/disk:ro \
      --publish=8080:8080 \
      --detach=true \
      --name=cadvisor \
      --privileged \
      --device=/dev/kmsg \
      gcr.io/cadvisor/cadvisor
   ```
2. 设置自动启动
    ```bash
    docker update --restart = always cadvisor
    ```
