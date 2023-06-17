# ESXI RDM 磁盘直通

## 设置 RDM 直通

- 开启 ESXI 主机的 ssh 服务
- ssh 连接 ESXI 主机
- ```bash
  vmkfstools -z [磁盘路径] [数据存储路径]/[磁盘文件名称].vmdk
  # example
  vmkfstools -z /vmfs/devices/disks/t10.ATA_____TOSHIBA_HDWE140_________________________________41J8K86KFBRG /vmfs/volumes/6300a399-8e448fa0-c392-b42e999d1004/HDD_4TB_TSB.vmdk
  ```
- 操作成功后无提示
- 数据存储中出现新的虚拟磁盘
