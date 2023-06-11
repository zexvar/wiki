---
title: Cadvisor 容器监控
---

## 获取镜像
* Docker hub 提供的镜像已经不再更新
* Google 官方提供的镜像需要特殊网络环境
* Github 下载二进制文件后自行构建镜像

[Github链接](https://github.com/google/cadvisor)

## 启动容器
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
--restart=always \
gcr.io/cadvisor/cadvisor
```
## 接入Prometheus

检查服务状态: http://ip:8080/metrics

修改Prometheus配置文件

```yaml title='prometheus.yml'
- job_name: 'cadvisor'
  static_configs:
    - targets: 
      - 'x.x.x.x:8080'
```