# Code Server 云端开发环境

## 准备工作

```bash
mkdir -p /opt/code-server/config
```

## 启动容器

```bash
docker run -d \
--name=code-server \
-e PASSWORD=password `#optional` \
# -e HASHED_PASSWORD= `#optional` \
-e SUDO_PASSWORD=password `#optional` \
# -e SUDO_PASSWORD_HASH= `#optional` \
-e DEFAULT_WORKSPACE=/config/workspace `#optional` \
-p 8443:8443 \
-v /opt/code-server/:/config \
--restart always \
lscr.io/linuxserver/code-server:latest
```

## 连接 Jupyter 内核需要 HTTPS

NGINX 反代配置

```
server {
    listen      443 ssl;
    listen [::]:443 ssl;

    location / {
        proxy_http_version 1.1;
        proxy_set_header Host $host;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection upgrade;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $http_x_forwarded_proto;
        proxy_pass http://127.0.0.1:8443;
    }
}
```
