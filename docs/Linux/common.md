# Linux 常用设置

## 常用软件安装

安装软件 : `apt install vim curl`

## 设置环境变量

以 anaconda 为例 : `export PATH=$PATH:/usr/local/anaconda3/bin`

## 设置时区

可以通过首字母快速搜索 : `dpkg-reconfigure tzdata`

## Python 版本设置

```bash
sudo update-alternatives --install /usr/bin/python python /usr/bin/python2 100
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 150
```

## SSH 免密登录

在客户机生产密钥对 (id_rsa, id_rsa.pub) : `ssh-keygen -t rsa`

将公钥内容添加到服务器机器 (id_rsa.pub)

```bash
cd /root/.ssh/
# echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDJXhPHzYyT8pkIIkACZ85KwgTA3/BuFNtj1qbOFvQvUU19Z9SIgZoCYZR+vhGKpLESmj9HnQydfDn6H5lqslsmyis2kXqSYtmYwDGRYERXtg+gLIHItlmJOGmNw5i6EAe24JXjlGZnmxP64TOQieDT/EdiE2g+Wdlg8JsAPGfdc/2gpqNuevRbIYCUJAiPTdXSZvYNVac+CIaxfeRwaED77iMbNX7mMCLGhHQSAbQjW7Tykyr6+fTFN1gc7OyJmMvptOU6dDxn4BL4XooNFVZv5Gl28UdPzdrwVYmFETRjIfkzY//QX9qS99p3d9g/lIITnti6H1RTI0AXS9MagRwRhGH4AwJHWDiUy/UquvnoTVCGJ5TN/mRznnc10qsmjrZXVGOkL5eq5SGYeIbvqvZD+8xj6BsFbyuWICvXnFA/6PpFPq8Fk35l4Aksgr3/09UD08LwDgzjMsSaSrrCdTfLCCYzBvL4xMEVpmlx0lewbNcF9ntuPyiLnIsqeD36VE8= root@Test" > authorized_keys
echo "ssh-rsa XXX" > authorized_keys
chmod 600 authorized_keys
```

注意确保 authorized_keys 文件权限为 600
