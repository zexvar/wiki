# SMB 端口转发

## 关闭冲突服务

```powershell
cmd /c sc config LanmanServer start=disabled
# reboot
shutdown -r 
```

## 配置端口转发

```powershell
netstat -ano | findstr "445"
# 确认输出为空

netsh interface portproxy add v4tov4 listenport=445 listenaddress=127.0.0.1 connectport=[smb port] connectaddress=[smb ip]
netsh interface portproxy add v6tov6 listenport=445 listenaddress=::1 connectport=[smb port] connectaddress=[smb ip]

# 查看转发结果
netsh interface portproxy show all
```

## 清除连接历史记录

删除远程磁盘历史记录 `regedit`

在注册表中定位到 `HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Map Network Drive MRU`
