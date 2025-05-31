# 媒体下载服务

## 配置文件

```yml title='docker-compose.yml'
services:
  qbit:
    image: linuxserver/qbittorrent
    container_name: qbit
    networks:
      - traefik
    ports:
      - 57891:57891
      - 57891:57891/udp
    volumes:
      - ./data/qbit:/config
      - downloads:/downloads
    environment:
      - TZ=Asia/Shanghai
      - TORRENTING_PORT=57891
      - DOCKER_MODS=ghcr.io/vuetorrent/vuetorrent-lsio-mod:latest
    labels:
      - traefik.enable=true
      - traefik.http.routers.qbit.rule=HostRegexp(`^qbit.*`)
      - traefik.http.services.qbit.loadbalancer.server.port=8080
    restart: always

  iyuu:
    image: iyuucn/iyuuplus-dev
    container_name: iyuu
    networks:
      - traefik
    volumes:
      - ./data/iyuu/data:/data
      - ./data/iyuu/config:/iyuu
    labels:
      - traefik.enable=true
      - traefik.http.routers.iyuu.rule=HostRegexp(`^iyuu.*`)
      - traefik.http.services.iyuu.loadbalancer.server.port=8780
    restart: always

networks:
  traefik:
    external: true

volumes:
  downloads:
    external: true
```
