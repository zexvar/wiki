# NFS 服务搭建和使用

## NFS 服务端搭建

### 安装并启动 NFS 服务

安装服务 `apt install nfs-kernel-server`

检查服务状态

```bash
systemctl status nfs-server
systemctl enable nfs-server
systemctl start nfs-server
```

### 修改服务配置

创建共享目录 `mkdir /nfs`

```bash title="/etc/exports"
/nfs 10.0.0.101(rw,sync,no_root_squash,no_subtree_check)
/nfs 10.0.0.*(rw,sync,no_root_squash,no_subtree_check)
/nfs 10.0.0.0/16(rw,sync,no_root_squash,no_subtree_check)
```

配置文件中的权限

* rw 允许读写
* sync 文件同时写入硬盘和内存
* no_subtree_check 即使输出目录是一个子目录,不检查其父目录的权限,这样可以提高效率

### 生效配置并检查

生效配置文件 : `exportfs -arv`

检查生效配置 : `showmount -e `

## NFS 客户端配置

### 安装 NFS 客户端

``` bash
apt install nfs-common
```

### 挂载 NFS 共享目录

客户端创建挂载点目录

``` bash
mkdir -p /nfs-mount
mount 10.0.0.100:/nfs /nfs-mount
```

### 开机自动挂载

```bash title="/etc/fstab"
10.0.0.30:/nfs     /nfs-mount       nfs     defaults  0  0
```

## 查看服务状态

``` bash
nfsstat
nfsstat -l
```