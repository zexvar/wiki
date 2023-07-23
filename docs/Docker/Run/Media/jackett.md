# Jackett 索引器

## 启动容器

使用 linuxserver 提供的镜像

```bash
docker run -d \
--name=jackett \
-e AUTO_UPDATE=true \
-p 9117:9117 \
-v /opt/jackett/:/config \
--restart always \
lscr.io/linuxserver/jackett:latest
```

## 添加索引

点击 `Add indexer` 选取需要的索引
