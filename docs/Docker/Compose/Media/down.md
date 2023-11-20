# 媒体下载服务

## 配置文件

```yaml title='docker-compose.yml'
version: "3.9"

services:
  qbittorrent:
    image: lscr.io/linuxserver/qbittorrent:latest
    container_name: qbittorrent
    network_mode: host
    volumes:
      - ./data/qbittorrent:/config
      - downloads_data:/downloads
    environment:
      - PUID=0
      - PGID=0
    restart: always

  aria2-pro:
    image: p3terx/aria2-pro
    container_name: aria2
    network_mode: host
    environment:
      - PUID=0
      - PGID=0
      - RPC_PORT=6800
      - RPC_SECRET=******
    volumes:
      - ./data/aria2:/config
      - downloads_data:/downloads
    restart: always

volumes:
  downloads_data:
    driver_opts:
      type: nfs
      o: addr=10.0.0.30,rw,nfsvers=4
      device: :/mnt/main/down
```
