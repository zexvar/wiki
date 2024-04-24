# 媒体下载服务

## 配置文件

```yml title='docker-compose.yml'
services:
  qbittorrent:
    image: linuxserver/qbittorrent
    container_name: qbittorrent
    network_mode: host
    volumes:
      - ./data/qbittorrent:/config
      - downloads_data:/downloads
    environment:
      - PUID=0
      - PGID=0
    restart: always

volumes:
  downloads_data:
    driver_opts:
      type: nfs
      o: addr=10.0.0.30,rw,nfsvers=4
      device: :/mnt/main/down
```
