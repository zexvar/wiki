# Rclone 挂载磁盘

## 创建 Rclone 配置

以 onedrive 为例子

- 添加`:shared`参数挂载到宿主机

## 配置文件

```yml title='docker-compose.yml'services:
rclone:
  image: rclone/rclone
  container_name: rclone
  network_mode: bridge
  privileged: true
  volumes:
    - /root/.config/rclone/:/config/rclone
    - /mnt/onedrive:/onedrive:shared
  command: >
    mount onedrive:/ /onedrive
    --allow-other
    --allow-non-empty
    --vfs-cache-mode full
    --vfs-cache-max-size 100G
  restart: always
```
