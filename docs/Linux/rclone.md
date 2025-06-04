# Rclone 常用命令

## Dedupe 去重命令

Rclone 提供多种 `--dedupe-mode` 模式来处理重复文件

| 模式          | 描述                                             |
| ------------- | ------------------------------------------------ |
| `interactive` | 互动模式：每次冲突时询问用户如何处理             |
| `skip`        | 删除完全相同的文件，跳过剩下的所有文件（不处理） |
| `first`       | 删除其他重复文件，仅保留第一个文件               |
| `newest`      | 删除其他重复文件，仅保留最新修改时间的文件       |
| `oldest`      | 删除其他重复文件，仅保留最早修改时间的文件       |
| `largest`     | 删除其他重复文件，仅保留文件大小最大的           |
| `smallest`    | 删除其他重复文件，仅保留文件大小最小的           |
| `rename`      | 删除重复文件，并将其余的文件重命名避免冲突       |
| `list`        | 仅列出重复文件，不进行任何修改                   |

> ⚠️ 使用 `--by-hash` 可以基于文件哈希值判断重复

常用参数说明

- -n, --dry-run：试运行无实际更改
- -i, --interactive：启用交互模式
- -v, --verbose：输出详细信息

```bash
# 列出重复文件（基于哈希）
rclone dedupe --by-hash --dedupe-mode list path

# 自动保留最新文件
rclone dedupe --by-hash --dedupe-mode newest path

# 自动保留最旧文件
rclone dedupe --by-hash --dedupe-mode oldest path
```

## Docker 配置文件

```yml title='docker-compose.yml'
services:
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
      --no-modtime
      --allow-other
      --allow-non-empty
      --vfs-cache-mode full
      --vfs-cache-max-age 24h
      --vfs-cache-max-size 50G
    restart: always
```
