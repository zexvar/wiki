# Zerotier 组网

> ZeroTier is a secure network overlay that allows you to manage all of your network resources as if they were on the same LAN. The software-defined solution can be deployed in minutes from anywhere. No matter how many devices you need to connect, or where they are in the world, ZeroTier makes global networking simple.

官网链接 [Zerotier](https://www.zerotier.com/)

## 准备工作

创建一个网络并复制网络 ID

## 配置文件

```yml title='docker-compose.yml'
services:
  zerotier:
    image: zerotier/zerotier
    container_name: zerotier
    network_mode: host
    cap_add:
      - NET_ADMIN
      - SYS_ADMIN
    devices:
      - /dev/net/tun
    volumes:
      - ./data/zerotier:/var/lib/zerotier-one/
    command: <NETWORK_ID>
    restart: always
```

## 批准登录

登录 Zerotier 控制台批准设备
