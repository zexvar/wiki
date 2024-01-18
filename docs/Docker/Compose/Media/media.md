# 媒体管理服务

## 配置文件

```yml title='docker-compose.yml'
version: "3.9"

services:
  flaresolverr:
    image: flaresolverr/flaresolverr:latest
    container_name: flaresolverr
    networks:
      - main
    labels:
      - traefik.enable=true
      - traefik.http.routers.flaresolver.entryPoints=web
      - traefik.http.routers.flaresolver.rule=HostRegexp(`{host:^flare.*}`)
      - traefik.http.services.flaresolver.loadbalancer.server.port=8191
    restart: always

  jackett:
    image: linuxserver/jackett:latest
    container_name: jackett
    networks:
      - main
    volumes:
      - ./data/jackett:/config
    environment:
      - TZ=Asia/Shanghai
      - AUTO_UPDATE=true
    labels:
      - traefik.enable=true
      - traefik.http.routers.jackett.entryPoints=web
      - traefik.http.routers.jackett.rule=HostRegexp(`{host:^jackett.*}`)
      - traefik.http.services.jackett.loadbalancer.server.port=9117
    restart: always

  prowlarr:
    image: linuxserver/prowlarr:latest
    container_name: prowlarr
    networks:
      - main
    volumes:
      - ./data/prowlarr:/config
    environment:
      - PUID=0
      - PGID=0
      - TZ=Asia/Shanghai
    labels:
      - traefik.enable=true
      - traefik.http.routers.prowlarr.entryPoints=web
      - traefik.http.routers.prowlarr.rule=HostRegexp(`{host:^prowlarr.*}`)
      - traefik.http.services.prowlarr.loadbalancer.server.port=9696
    restart: always

  radarr:
    image: linuxserver/radarr:latest
    container_name: radarr
    networks:
      - main
    volumes:
      - ./data/radarr:/config
      - downloads_data:/downloads
    environment:
      - PUID=0
      - PGID=0
      - TZ=Asia/Shanghai
    labels:
      - traefik.enable=true
      - traefik.http.routers.radarr.entryPoints=web
      - traefik.http.routers.radarr.rule=HostRegexp(`{host:^radarr.*}`)
      - traefik.http.services.radarr.loadbalancer.server.port=7878
    restart: always

  sonarr:
    image: linuxserver/sonarr:latest
    container_name: sonarr
    networks:
      - main
    volumes:
      - ./data/sonarr:/config
      - downloads_data:/downloads
    environment:
      - PUID=0
      - PGID=0
      - TZ=Asia/Shanghai
    labels:
      - traefik.enable=true
      - traefik.http.routers.sonarr.entryPoints=web
      - traefik.http.routers.sonarr.rule=HostRegexp(`{host:^sonarr.*}`)
      - traefik.http.services.sonarr.loadbalancer.server.port=8989
    restart: always

networks:
  main:
    external: true

volumes:
  downloads_data:
    driver_opts:
      type: nfs
      o: addr=10.0.0.30,rw,nfsvers=4
      device: :/mnt/main/down
```
