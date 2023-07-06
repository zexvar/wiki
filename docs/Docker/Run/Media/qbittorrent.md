# QBittorrent 下载工具

## 准备工作

`mkdir -p /opt/qbittorrent/config`

## 运行容器

/mnt/down 为宿主机下载的文件保存位置

```bash
docker run -d \
--name=qbittorrent \
-e PUID=0 \
-e PGID=0 \
-e WEBUI_PORT=8080 \
-p 8080:8080 \
-p 6881:6881 \
-p 6881:6881/udp \
-v /opt/qbittorrent/config:/config \
-v /mnt/down:/downloads \
--restart always \
lscr.io/linuxserver/qbittorrent:latest
```

## 宿主机网络

通过此方式可以直接支持 IPV6 上传与下载

```bash
docker run -d \
--name=qbittorrent \
--network=host \
-e PUID=0 \
-e PGID=0 \
-e TZ=Asian/Shanghai \
-e WEBUI_PORT=8080 \
-v /opt/qbittorrent/config:/config \
-v /mnt/down:/downloads \
--restart=always \
lscr.io/linuxserver/qbittorrent:latest
```
