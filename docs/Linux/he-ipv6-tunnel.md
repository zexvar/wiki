# HE IPv6 隧道

## 本文目标

部分云主机仅有 IPV4 地址,通过 HE Tunnel Broker 为其添加 IPV6 地址.

## 创建隧道

在 Tunnel Broker 官网注册账号

- [HE Tunnel Broker 官网](https://tunnelbroker.net/)

登录账号并创建隧道,点击 `Create Regular Tunnel` 按钮.

输入 VPS 的 `IPV4` 地址并选择合适的节点.

## 配置网络参数

修改网络配置

在 `Example Configurations` 中选择对应的操作系统

将显示的网络配置内容添加到主机中

重启主机 `reboot`

## 测试 IPV6 是否正常

```bash
root@vps:~# ping 6.ipw.cn
PING 6.ipw.cn(2402:4e00:1013:e500:0:9671:f018:4947 (2402:4e00:1013:e500:0:9671:f018:4947)) 56 data bytes
64 bytes from 2402:4e00:1013:e500:0:9671:f018:4947 (2402:4e00:1013:e500:0:9671:f018:4947): icmp_seq=1 ttl=49 time=370 ms
64 bytes from 2402:4e00:1013:e500:0:9671:f018:4947 (2402:4e00:1013:e500:0:9671:f018:4947): icmp_seq=2 ttl=49 time=373 ms
64 bytes from 2402:4e00:1013:e500:0:9671:f018:4947 (2402:4e00:1013:e500:0:9671:f018:4947): icmp_seq=3 ttl=49 time=386 ms
64 bytes from 2402:4e00:1013:e500:0:9671:f018:4947 (2402:4e00:1013:e500:0:9671:f018:4947): icmp_seq=4 ttl=49 time=391 ms
```
