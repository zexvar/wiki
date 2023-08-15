# Windows 开发环境设置

## 常见 SDK 下载

通过 winget 包管理器一键配置

|        | winget                                  |
| ------ | --------------------------------------- |
| java   | `winget install BellSoft.LibericaJDK.8` |
| python | `winget install Python.Python.3.9`      |
| nodejs | `winget install OpenJS.NodeJS.LTS`      |

## 常用工具下载

- vim `winget install vim.vim`
- git `winget install Git.Git --interactive`

vim 安装完成后需要手动设置环境变量

```shell
# 为 git 设置代理
git config --global http.proxy socks5://127.0.0.1:10808
git config --global https.proxy socks5://127.0.0.1:10808
```

添加 `--interactive` 参数可以完全控制安装过程

## win 下配置 curl

通过设置 PowerShell Profile 删除系统自带别名

允许加载自定义 Profile `set-executionpolicy remotesigned`

| 作用范围          | Profile 位置                                                |
| ----------------- | ----------------------------------------------------------- |
| 所有用户 所有主机 | $PSHOME\Profile.ps1                                         |
| 所有用户 当前主机 | $PSHOME\Microsoft.PowerShell_profile.ps1                    |
| 当前用户 所有主机 | $HOME\Documents\PowerShell\Profile.ps1                      |
| 当前用户 当前主机 | $HOME\Documents\PowerShell\Microsoft.PowerShell_profile.ps1 |

```bash title="C:\Windows\System32\WindowsPowerShell\v1.0\Profile.ps1"
# $PSHOME\Profile.ps1。
del alias:curl
```

- 若命令不存在

通过 winget 安装 curl

```bash
winget install cURL.cURL
```

## WSL 默认 root 用户

以debian为例 `debian config --default-user root`
