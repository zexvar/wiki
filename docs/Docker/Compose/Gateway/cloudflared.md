# Cloudflared 内网穿透

## 服务作用

利用 Cloudflared Tunnels 暴露内网服务
通过 Cloudflare Zero Trust Warp 组网

## 配置文件

```yml
cloudflared:
  container_name: cloudflared
  image: cloudflare/cloudflared
  network_mode: host
  command: tunnel --no-autoupdate --protocol auto run --token ******
  restart: always
```

## 注意事项

- 默认使用 quic 协议通信
- 运营商对 quic 协议存在阻断
- 通过添加 `--protocol auto` 参数
- 在 quic 协议失败时切换到 http 协议
