# SMB 服务搭建和使用

## SMB 服务端配置

### 安装 SMB 服务端

安装服务 `apt install samba`

### 修改服务配置

创建共享目录 `mkdir /smb && chmod -R 777 /smb`

修改配置文件

```ini title="/etc/samba/smb.conf"
[samba]
comment = Share Directories
path = /smb
public = yes
writable = yes
browseable = yes
create mask = 777
directory mask = 777
```

### 添加访问用户

添加用户admin

```bash
useradd admin
smbpasswd -a admin
```

### 启动 SMB 服务

```bash
service smbd start      #启动
service smbd stop       #停止
service smbd restart    #重启
```

## SMB 客户端挂载

### 安装 SMB 客户端

安装客户端 `apt install cifs-utils`

### 创建挂载点并挂载

```bash
mkdir /share
mount //xx.xx.xx.xx/smb /smb -o username=admin,password=123456,uid=0,gid=0
```

### 开机自动挂载 

```bash title="/etc/fstab"
//xx.xx.xx.xx/smb /smb/ cifs defaults,username=admin,password=123456,uid=0,gid=0 0 0
```
