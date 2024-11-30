# Windows 常用设置优化

## 激活系统

> 根据系统版本版本选择密钥

| Operating system edition                      | KMS Client Product Key        |
| --------------------------------------------- | ----------------------------- |
| Windows 10 Professional                       | W269N-WFGWX-YVC9B-4J6C9-T83GX |
| Windows Server 2025 Standard                  | TVRH6-WHNXV-R9WG3-9XRFY-MY832 |
| Windows Server 2025 Datacenter                | D764K-2NDRG-47T6Q-P8T8W-YP6DF |
| Windows Server 2025 Datacenter: Azure Edition | XGN3F-F394H-FD2MY-PP6FD-8MCRC |

管理员权限运行

```bash
# 卸载旧的密钥
slmgr.vbs /upk
# 安装密钥
slmgr /ipk W269N-WFGWX-YVC9B-4J6C9-T83GX
slmgr /skms www.zoxe.top
slmgr /ato
```

## 添加休眠电源选项

1. 打开控制面板
2. 硬件和声音-> 电源选项 `控制面板\所有控制面板项\电源选项`
3. 选择电源按钮的功能 -> 更改当前不可用的设置 -> 勾选 `休眠` 选项

## 开启默认管理员权限

1. WIN + R 输入 `secpol.msc` 打开本地安全策略 (专业版 WINDOWS)

2. 安全设置 -> 本地策略 -> 安全选项 -> 用户帐户控制：以管理员批准模式运行所有管理员 -> 已禁用

3. 重启系统使设置生效
