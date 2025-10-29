
[ScoopInstaller/Scoop: A command-line installer for Windows.](https://github.com/ScoopInstaller/Scoop)

在 Windows 下，搭建开发环境一直是一个复杂且困难的问题。由于没有一个统一的标准，导致各种开发环境的安装方式差异巨大，需要付出很多不必要的时间成本。而 Scoop 可以帮助你统一安装并管理常见的开发软件，省去了手动下载安装，配置环境变量等繁琐步骤。

例如安装 python 和 nodejs 只需要执行：

```powershell
scoop install python
scoop install nodejs
```

## 使用 Scoop

Scoop 的官方文档对于新手非常友好，相对于在此处赘述更推荐阅读 [官方文档](https://github.com/ScoopInstaller/Scoop) 或 [快速入门](https://github.com/ScoopInstaller/Scoop/wiki/Quick-Start) 。

# 安装java

### 首先，安装必要的bucket:

`scoop bucket add versions`

`scoop bucket add java`

### 接下来，安装OpenJDK:

`scoop install openjdk`

### 验证Java是否安装成功:

`java —version`

## 卸载java

`scoop uninstall openjdk`

## 安装其他版本的java

`scoop install openjdk@17`

## 切换版本

`scoop reset openjdk17`