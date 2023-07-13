# Frp 内网穿透

## 部署 frp 服务端

创建 frps.ini 配置文件

```bash
mkdir -p /opt/frp
vim /opt/frp/frps.ini
```

文件内容如下

```ini
[common]
bind_addr = 0.0.0.0
bind_port = 7000
kcp_bind_port = 7000
# quic_bind_port = 7000
# use_compression = true
use_encryption = true
max_pool_count = 5
vhost_http_port = 80
vhost_https_port = 443

#客户端秘钥
token = 123456
dashboard_port = 7500
enable_prometheus = true
```

若需要开启 Prometheus 添加`enable_prometheus = true`

需要放行端口 80/443/7000 等

运行容器

```bash
docker run -d \
--network host  \
-v /opt/frp/frps.ini:/etc/frp/frps.ini \
--name frps \
--restart=always \
snowdreamtech/frps
```

## 部署 frp 客户端

创建 frpc.ini 配置文件

```bash
mkdir -p /op/frp
vim /opt/frp/frpc.ini
```

文件内容如下

```ini
[common]
server_addr = server
server_port = 7000
protocol = kcp
pool_count = 3
token = 123456

[http]
type = http
local_port = 80
local_ip = 127.0.0.1
custom_domains = *

[https]
type = https
local_port = 443
local_ip = 127.0.0.1
custom_domains = *
```

运行容器

```bash
docker run --restart=always --network host -d -v /opt/frp/frpc.ini:/etc/frp/frpc.ini --name frpc snowdreamtech/frpc
```

## 查看服务状态

访问 http://server:7500 进入 frp 控制台

输入密码后在 Proxies 目录中查看已经建立的隧道
