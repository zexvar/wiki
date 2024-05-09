# Owncloud 云盘

## 配置文件

```yml title='docker-compose.yml'
services:
  owncloud:
    image: owncloud/server
    container_name: owncloud
    networks:
      - main
    volumes:
      - ./data/owncloud/:/mnt/data
    environment:
      # database
      - OWNCLOUD_DB_TYPE=mysql
      - OWNCLOUD_DB_HOST=mysql
      - OWNCLOUD_DB_NAME=owncloud
      - OWNCLOUD_DB_USERNAME=root
      - OWNCLOUD_DB_PASSWORD=******
      - OWNCLOUD_MYSQL_UTF8MB4=true
      # memcache
      - OWNCLOUD_REDIS_ENABLED=true
      - OWNCLOUD_REDIS_HOST=redis
      - OWNCLOUD_ADMIN_USERNAME=admin
      - OWNCLOUD_ADMIN_PASSWORD=******
      - OWNCLOUD_DOMAIN=******
      #- OWNCLOUD_TRUSTED_DOMAINS=***,***
      - TZ=Asia/Shanghai
    labels:
      - traefik.enable=true
      - traefik.http.routers.owncloud.rule=HostRegexp(`^cloud.*`)
      - traefik.http.services.owncloud.loadbalancer.server.port=8080
    restart: always

networks:
  main:
    external: true
```
