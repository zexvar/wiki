---
title: Docker Watchtower 更新容器
description: 
published: true
date: 2023-02-11T13:24:07.214Z
tags: docker, upgrade, watchtower
editor: markdown
dateCreated: 2022-11-04T13:20:27.400Z
---

## 更新所有容器

```bash
docker run --rm \
-v /var/run/docker.sock:/var/run/docker.sock \
containrrr/watchtower \
--run-once -c
```
* -c 升级后删除旧的docker镜像

## 指定容器名进行更新

```bash
docker run --rm \
-v /var/run/docker.sock:/var/run/docker.sock \
containrrr/watchtower \
--run-once -c container_name
```
* -c 升级后删除旧的docker镜像
* container_name 为需要被升级的容器名
