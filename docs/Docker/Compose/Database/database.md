# 数据库服务

## 配置文件

```yml title='docker-compose.yml'
services:
  mysql:
    image: mysql
    container_name: mysql
    networks:
      - main
    ports:
      - 3306:3306
    volumes:
      - ./data/mysql/logs:/var/log/mysql
      - ./data/mysql/data:/var/lib/mysql
      #- ./data/mysql/my.cnf:/etc/mysql/my.cnf
    environment:
      - MYSQL_ROOT_PASSWORD=******
      - TZ=Asia/Shanghai
    restart: always

  redis:
    image: redis
    container_name: redis
    networks:
      - main
    ports:
      - 6379:6379
    volumes:
      - ./data/redis/data:/data
      #- ./data/redis/conf/redis.conf:/etc/redis/redis.conf
    #command: redis-server /etc/redis/redis.conf
    environment:
      - TZ=Asia/Shanghai
    restart: always

networks:
  main:
    external: true
```
