# Docker Network 特殊配置

## 修改配置

根据 `Docker Engine version 27` 更新内容当前版本无需修改配置

- `ip6tables` is no longer experimental. You may remove the experimental configuration option and continue to use IPv6, if it is not required by any other features.
- `ip6tables` is now enabled for Linux bridge networks by default.

## 先前版本

对于 Docker Engine version 27 之前版本

- 编辑位于 `/etc/docker/daemon.json` 的配置文件

  ```json
  {
    "ip6tables": true,
    "experimental": true
  }
  ```

- 配置生效 `systemctl restart docker`

## 创建 IPV6 网络

- 创建网络 `docker network create --ipv6 ip6net`
- 指定网段 `docker network create --ipv6 --subnet fd00::/64 ip6net`

- 在 docker-compose.yml 中添加

  ```yml
  networks:
  ip6net:
    external: true
  ```
