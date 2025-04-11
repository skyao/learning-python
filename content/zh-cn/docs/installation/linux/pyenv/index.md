---
title: "使用 pyenv 安装"
linkTitle: "pyenv"
weight: 10
date: 2025-03-13
description: >
  使用 pyenv 在 linux 上安装多个版本的 python
---

以 debian 12 为例，通过 pyenv 安装多个版本的 python。

## 安装 pyenv

### pyenv 介绍

pyenv 是一个简单的 python 版本管理工具，官网地址：

https://github.com/pyenv/pyenv

### pyenv 安装

参考 pyenv 的官方安装文档：

https://github.com/pyenv/pyenv?tab=readme-ov-file#linuxunix

执行安装命令：

```bash
curl -fsSL https://pyenv.run | bash
```

输出为：

```bash
Cloning into '/home/sky/.pyenv'...
remote: Enumerating objects: 1363, done.
remote: Counting objects: 100% (1363/1363), done.
remote: Compressing objects: 100% (724/724), done.
remote: Total 1363 (delta 824), reused 806 (delta 506), pack-reused 0 (from 0)
Receiving objects: 100% (1363/1363), 1.14 MiB | 5.63 MiB/s, done.
Resolving deltas: 100% (824/824), done.
Cloning into '/home/sky/.pyenv/plugins/pyenv-doctor'...
remote: Enumerating objects: 11, done.
remote: Counting objects: 100% (11/11), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 11 (delta 1), reused 5 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (11/11), 38.72 KiB | 619.00 KiB/s, done.
Resolving deltas: 100% (1/1), done.
Cloning into '/home/sky/.pyenv/plugins/pyenv-update'...
remote: Enumerating objects: 10, done.
remote: Counting objects: 100% (10/10), done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 10 (delta 1), reused 5 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (10/10), done.
Resolving deltas: 100% (1/1), done.
Cloning into '/home/sky/.pyenv/plugins/pyenv-virtualenv'...
remote: Enumerating objects: 64, done.
remote: Counting objects: 100% (64/64), done.
remote: Compressing objects: 100% (57/57), done.
Receiving objects: 100% (64/64), 43.08 KiB | 1.08 MiB/s, done.
remote: Total 64 (delta 10), reused 23 (delta 0), pack-reused 0 (from 0)
Resolving deltas: 100% (10/10), done.

WARNING: seems you still have not added 'pyenv' to the load path.

# Load pyenv automatically by appending
# the following to
# ~/.bash_profile if it exists, otherwise ~/.profile (for login shells)
# and ~/.bashrc (for interactive shells) :

export PYENV_ROOT="$HOME/.pyenv"
[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init - bash)"

# Restart your shell for the changes to take effect.

# Load pyenv-virtualenv automatically by adding
# the following to ~/.bashrc:

eval "$(pyenv virtualenv-init -)"

```

pyenv 被安装在目录 "$HOME/.pyenv"，遵循上面的提示，

```bash
vi ~/.zshrc
```

增加如下内容：

```bash
export PYENV_ROOT="$HOME/.pyenv"
[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init - zsh)"
```

> 备注：注意修改 bash 为 zsh，因为我一般默认用 zsh。这里如果没有改过来，后面安装完成后 path 路径会有问题。

执行 

```bash
source ~/.zshrc
```

重新装载，然后验证一下：

```bash
pyenv --version
```

输出为：

```bash
pyenv 2.5.3
```

## 安装 python

### 准备工作

python 安装时需要使用 zlib，首先安装：

```bash
sudo apt install zlib1g-dev libbz2-dev libncurses-dev libffi-dev libreadline-dev libssl-dev libsqlite3-dev liblzma-dev
```

否则会报错：

```bash
ModuleNotFoundError: No module named 'zlib'
ModuleNotFoundError: No module named '_bz2'
ModuleNotFoundError: No module named '_curses'
ModuleNotFoundError: No module named '_ctypes'
ModuleNotFoundError: No module named 'readline'
ModuleNotFoundError: No module named '_ssl'
ModuleNotFoundError: No module named '_sqlite3'
ModuleNotFoundError: No module named '_lzma'
```

安装完成之后，验证一下：

```bash
python3 -c "import bz2; import curses; import ctypes; import readline; import ssl; print('All modules loaded successfully')"
```

如果没有报错，则输出为：

```bash
All modules loaded successfully
```

### pyenv 命令

通过下面的命令可以看到 pyenv 可以安装的版本列表：

```bash
pyenv install -l
```

内容太多了，按照版本 grep 一下，如看看 3.11.x 版本：

```bash
pyenv install -l | grep 3.11
```

### 安装 3.11 版本

```bash
pyenv install -l | grep 3.11
```

发现 3.11 系列最新的是 3.11.11 版本。

安装 python 3.11.11 版本：

```bash
pyenv install 3.11.11
```

输出为：

```bash
Downloading Python-3.11.11.tar.xz...
-> https://www.python.org/ftp/python/3.11.11/Python-3.11.11.tar.xz
Installing Python-3.11.11...
Installed Python-3.11.11 to /home/sky/.pyenv/versions/3.11.11
```

设置 3.11.1 为全局默认版本：

```bash
pyenv global 3.11.11
```

验证一下 python 版本：

```bash
$ python3 --version
Python 3.11.11
$ python --version
Python 3.11.9
```

此时通过 `pyenv versions` 命令可以看到系统中只安装了一个 3.11.11 版本和一个系统自带的版本（system）：

```bash
$ pyenv versions
pyenv versions
  system
* 3.11.11 (set by /home/sky/.pyenv/version)
```

此时 pip 版本信息如下：

```bash
$ pip --version
pip 24.0 from /home/sky/.pyenv/versions/3.11.11/lib/python3.11/site-packages/pip (python 3.11)

$ pip3 --version
pip 24.0 from /home/sky/.pyenv/versions/3.11.11/lib/python3.11/site-packages/pip (python 3.11)
```

### 安装 3.10 版本

```bash
pyenv install -l | grep 3.10
```

发现 3.10 系列最新的是 3.10.16 版本：

```bash
pyenv install 3.10.16
```

### 安装 3.12 版本

```bash
pyenv install -l | grep 3.12
```

发现 3.12 系列最新的是 3.12.9 版本：

```bash
pyenv install 3.12.9
```

### 切换版本

pyenv 的 shell 命令用来在当前 shell 中临时设置 python 版本，覆盖 global 设置：

```bash
$ pyenv versions
  system
  3.10.16
* 3.11.11 (set by /home/sky/.pyenv/version)
  3.12.9

$ python3 --version
Python 3.11.11

$ pyenv shell 3.12.9

$ pyenv versions
  system
  3.10.16
  3.11.11
* 3.12.9 (set by PYENV_VERSION environment variable)

$ python3 --version
Python 3.12.9
```

pyenv global 命令修改全局默认配置，注意这个修改不会立即生效，需要退出当前 shell 重新打开：

```bash
$ pyenv global 3.10.16

# 不直接生效
$ pyenv versions
  system
  3.10.16
  3.11.11
* 3.12.9 (set by PYENV_VERSION environment variable)

# 退出当前 shell 重新打开
$ pyenv versions
  system
* 3.10.16 (set by /home/sky/.pyenv/version)
  3.11.11
  3.12.9

$ python3 --version
Python 3.10.16

$ pip --version
pip 23.0.1 from /home/sky/.pyenv/versions/3.10.16/lib/python3.10/site-packages/pip (python 3.10)
```

