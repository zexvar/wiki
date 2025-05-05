# Debian 常用设置

## 换源

```shell
sed -i 's|deb.debian.org|mirrors.aliyun.com|g' /etc/apt/sources.list
sed -i 's|security.debian.org|mirrors.aliyun.com|g' /etc/apt/sources.list
```

## 网络设置

```shell
source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
allow-hotplug ens192
iface ens192 inet static
address 10.0.0.250
netmask 255.0.0.0
gateway 10.0.0.1
metric 0

iface ens192 inet6 auto
```
