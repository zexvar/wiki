# Docker Network 特殊配置

## 创建 IPV6 网络

- 编辑位于 `/etc/docker/daemon.json` 的配置文件

  ```json
  {
    "ip6tables": true,
    "experimental": true
  }
  ```

- 配置生效 `systemctl restart docker`

- 创建网络 `docker network create --ipv6 --subnet fd00::/64 main`

- 在 docker-compose.yml 中添加

  ```yml
  networks:
  main:
    external: true
  ```
