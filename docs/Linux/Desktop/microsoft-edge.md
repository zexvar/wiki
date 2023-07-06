# Microsoft Edge 安装

## 安装所需的软件包

```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common wget -y
```

## 添加 GPG 和官方源

```bash
# GPG
sudo wget -O- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | sudo tee /usr/share/keyrings/microsoft-edge.gpg
# 官方源
echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/microsoft-edge.gpg] https://packages.microsoft.com/repos/edge stable main' | sudo tee /etc/apt/sources.list.d/microsoft-edge.list
```

## 安装 edge

```
sudo apt update
sudo apt install microsoft-edge-stable
```
