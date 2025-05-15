# 媒体管理服务

## 创建挂载卷

```shell
docker volume create --driver local \
--opt type=nfs \
--opt o=addr=10.0.0.30,rw,nfsvers=4 \
--opt device=:/mnt/main/down \
downloads
```

## 配置文件

```yml title='docker-compose.yml'
services:
  flaresolverr:
    image: flaresolverr/flaresolverr
    container_name: flaresolverr
    networks:
      - traefik
    labels:
      - traefik.enable=true
      - traefik.http.routers.flaresolver.rule=HostRegexp(`^flare.*`)
      - traefik.http.services.flaresolver.loadbalancer.server.port=8191
    restart: always

  jackett:
    image: linuxserver/jackett
    container_name: jackett
    networks:
      - traefik
    volumes:
      - ./data/jackett:/config
    environment:
      - TZ=Asia/Shanghai
    labels:
      - traefik.enable=true
      - traefik.http.routers.jackett.rule=HostRegexp(`^jackett.*`)
      - traefik.http.services.jackett.loadbalancer.server.port=9117
    restart: always

  prowlarr:
    image: linuxserver/prowlarr
    container_name: prowlarr
    networks:
      - traefik
    volumes:
      - ./data/prowlarr:/config
    environment:
      - TZ=Asia/Shanghai
    labels:
      - traefik.enable=true
      - traefik.http.routers.prowlarr.rule=HostRegexp(`^prowlarr.*`)
      - traefik.http.services.prowlarr.loadbalancer.server.port=9696
    restart: always

  radarr:
    image: linuxserver/radarr
    container_name: radarr
    networks:
      - traefik
    volumes:
      - ./data/radarr:/config
      - downloads:/downloads
    environment:
      - TZ=Asia/Shanghai
    labels:
      - traefik.enable=true
      - traefik.http.routers.radarr.rule=HostRegexp(`^radarr.*`)
      - traefik.http.services.radarr.loadbalancer.server.port=7878
    restart: always

  sonarr:
    image: linuxserver/sonarr
    container_name: sonarr
    networks:
      - traefik
    volumes:
      - ./data/sonarr:/config
      - downloads:/downloads
    environment:
      - TZ=Asia/Shanghai
    labels:
      - traefik.enable=true
      - traefik.http.routers.sonarr.rule=HostRegexp(`^sonarr.*`)
      - traefik.http.services.sonarr.loadbalancer.server.port=8989
    restart: always

networks:
  traefik:
    external: true

volumes:
  downloads:
    external: true
```
