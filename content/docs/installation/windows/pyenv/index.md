---
title: "使用 pyenv 安装"
linkTitle: "pyenv"
weight: 20
date: 2025-02-02
description: >
  使用 pyenv 在 windows 上安装多个版本的 python
---

## pyenv

### pyenv 介绍

pyenv 是一个简单的 python 版本管理工具，官网地址：

https://github.com/pyenv/pyenv

pyenv 的官网说明：

> Pyenv 并不正式支持 Windows，也不能在 Windows 的 Linux 子系统之外的 Windows 环境中运行。此外，即使在 Windows 下，它所安装的 Pythons 也不是原生的 Windows 版本，而是在虚拟机中运行的 Linux 版本，因此你不会获得 Windows 特有的功能。
> 
> 如果您使用的是 Windows，我们建议您使用 @kirankotari 的 pyenv-win fork，它可以安装原生的 Windows Python 版本。

因此在 windows 平台上，要使用 pyenv-win：

https://github.com/pyenv-win/pyenv-win/

### pyenv 安装

参考 pyenv-win 的官方安装文档：

https://github.com/pyenv-win/pyenv-win/blob/master/docs/installation.md

打开 cmd，执行命令：

```bash
git clone https://github.com/pyenv-win/pyenv-win.git "%USERPROFILE%\.pyenv"
```

增加如下环境变量：

- PYENV="C:\Users\sky\.pyenv\pyenv-win\"
- PYENV_HOME="C:\Users\sky\.pyenv\pyenv-win\"
- PYENV_ROOT="C:\Users\sky\.pyenv\pyenv-win\"

修改 PATH 环境变量，增加两个路径：

- %USERPROFILE%\.pyenv\pyenv-win\bin
- %USERPROFILE%\.pyenv\pyenv-win\shims

重新打开 cmd 或者 git-bash，验证一下：

```bash
$ pyenv --version
pyenv 3.1.1
```

## 安装 python

### pyenv 命令

通过下面的命令可以看到 pyenv 可以安装的版本列表：

```bash
pyenv install -l
```

内容太多了，按照版本 grep 一下，如看看 3.11.x 版本：

```bash
pyenv install -l | grep 3.11
```

### 安装 3.11.9 版本

安装 python 3.11.9 版本：

```bash
pyenv install 3.11.9
```

输出为：

```bash
:: [Info] ::  Mirror: https://www.python.org/ftp/python
:: [Info] ::  Mirror: https://downloads.python.org/pypy/versions.json
:: [Info] ::  Mirror: https://api.github.com/repos/oracle/graalpython/releases
:: [Downloading] ::  3.11.9 ...
:: [Downloading] ::  From https://www.python.org/ftp/python/3.11.9/python-3.11.9-amd64.exe
:: [Downloading] ::  To   C:\Users\sky\.pyenv\pyenv-win\install_cache\python-3.11.9-amd64.exe
:: [Installing] ::  3.11.9 ...
:: [Info] :: completed! 3.11.9
```

设置 3.11.9 为全局默认版本：

```bash
pyenv global 3.11.9
```

验证一下 python 版本：

```bash
$ python3 --version
Python 3.11.9
$ python --version
Python 3.11.9
```

此时通过 `pyenv versions` 命令可以看到系统中只安装了一个 3.11.9 版本：

```bash
$ pyenv versions
* 3.11.9 (set by C:\Users\sky\.pyenv\pyenv-win\version)
```

此时 pip 版本信息如下：

```bash
$ pip --version
pip 24.0 from C:\Users\sky\.pyenv\pyenv-win\versions\3.11.9\Lib\site-packages\pip (python 3.11)
```

### 安装 3.10.11 版本

安装 python 3.10.11 版本：

```bash
pyenv install 3.10.11
```

### 安装 3.12.8 版本

安装 python 3.12.8 版本：

```bash
pyenv install 3.12.8
```

### 切换版本

pyenv 的 shell 命令本来是用来在当前 shell 中临时设置 python 版本，覆盖 global 设置。但是不知道为什么在 windows 下这个命名不能生效：

```bash
$ pyenv versions
  3.10.11
* 3.11.9 (set by C:\Users\sky\.pyenv\pyenv-win\version)
  3.12.8

$ python3 --version
Python 3.11.9

$ code pyenv shell 3.12.8

$ pyenv versions
  3.10.11
* 3.11.9 (set by C:\Users\sky\.pyenv\pyenv-win\version)
  3.12.8

$ python3 --version
Python 3.11.9
```

因此只好通过 pyenv global 命令来修改了，只是这样每次用的时候要注意先确认当前到底设置为哪个版本了。

```bash
$ pyenv global 3.12.8

$ pyenv versions
  3.10.11
  3.11.9
* 3.12.8 (set by C:\Users\sky\.pyenv\pyenv-win\version)

$ python3 --version
Python 3.12.8

$ pip --version
pip 24.3.1 from C:\Users\sky\.pyenv\pyenv-win\versions\3.12.8\Lib\site-packages\pip (python 3.12)
```