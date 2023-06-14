---
title: ESXI SATA控制器直通
---

## 直通起因
在 RDM 直通磁盘后,Truenas 等无法读取磁盘温度和S.M.A.R.T信息 

因此考虑直通 SATA 控制器给 Truenas

## 设置主机

- 选择要直通的 SATA 控制器,设置切换直通

| 属性      | 值                                      |
| --------- | --------------------------------------- |
| 设备名    | ASMedia Technology Inc. SATA controller |
| 设备 ID   | 0x1166                                  |
| 供应商 ID | 0x1b21                                  |

- 管理 -> 系统 -> 高级设置 -> 设置VMkernel.Boot.disableACSCheck值为true

## 修改主机直通设置
- 开启 ESXI 主机的 ssh 服务
- ssh 连接 ESXI 主机
- 修改passthru.map文件 `vi /etc/vmware/passthru.map`
- 在末尾添加`供应商id 设备id d3d0     false`
	```ini
  # PCIE SATA Controller
  1b21  1166  d3d0     false
  ```
- 去掉0x后的值即为所需要的id 

- 重启Esxi主机即可