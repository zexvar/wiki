# Jellyfin 影音服务器

## 镜像信息

使用镜像为 `linuxserver/jellyfin`

镜像硬件加速支持: `Intel` `Nvidia` ...

[Docker hub 链接](https://hub.docker.com/r/linuxserver/jellyfin)

## 硬件加速

安装 NVIDIA Container Toolkit
NVIDIA Container Toolkit 能够为容器使用 Nvidia GPU 加速提供支持

```bash
# 检查安装状态
docker run --rm --gpus all nvidia/cuda:11.4.3-base-ubuntu20.04 nvidia-smi
```

## 运行容器

```bash
docker run -d \
--name=jellyfin \
-e PGID=0 \
-e PUID=0 \
-p 8096:8096 \
-v /opt/jellyfin/config:/config \
-v /mnt/down/:/downloads \
--restart=always \
--runtime=nvidia \
-e NVIDIA_VISIBLE_DEVICES=all \
lscr.io/linuxserver/jellyfin:latest
```
