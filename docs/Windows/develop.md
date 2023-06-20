# Windows 常用开发环境

## 常见 SDK 下载

通过 winget 包管理器一键配置
|        | winget                                  |
| ------ | --------------------------------------- |
| java   | `winget install BellSoft.LibericaJDK.8` |
| python | `winget install Python.Python.3.9`      |
| nodejs | `winget install OpenJS.NodeJS.LTS`      |

## 常用工具下载

- git `winget install Git.Git`
- vim `winget install vim.vim`

## win 下配置 curl 和 wget

- 设置 powershell profile 删除系统自带别名

```bash
# C:\Windows\System32\WindowsPowerShell\v1.0
del alias:curl
del alias:wget
```

- 通过 winget 安装 curl 和 wget

```bash
winget install cURL.cURL
winget install JernejSimoncic.Wget
```
