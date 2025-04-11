---
title: "[不推荐]直接安装python"
linkTitle: "[不推荐]直接安装"
weight: 10
date: 2025-02-02
description: >
  使用二进制文件直接在 windows 上安装特定版本的 python
---

{{% alert title="警告" color="warning" %}}
不推荐直接安装 python，最好通过 pyenv 或者 anaconda 来安装和管理多个 python 版本。
{{% /alert %}}

### 下载

https://www.python.org/ftp/python/

从这个网址可以下载到各个版本的 python 安装文件，比如常见的 3.10/3.11/3.12 版本：

- [3.10.11](https://www.python.org/ftp/python/3.10.11/)
- [3.11.9](https://www.python.org/ftp/python/3.11.9/)
- [3.12.8](https://www.python.org/ftp/python/3.12.8/)

下载对应版本的 python-3.xx.x-amd64.exe 文件即可。

### 安装

通过下载的 python-3.xx.x-amd64.exe 文件安装。

安装过程选自定义安装，然后记得勾选自动设置windows环境变量。

安装完成后，在 cmd 中验证版本：

```bash
$ pip --version
pip 23.0.1 from D:\work\soft\python\lib\site-packages\pip (python 3.10)

$ python --version
Python 3.10.11
```

### 问题

直接安装是最简单最直接的方式，但只能安装一个版本，当遇到需要多个 python 版本时就麻烦了。

因此，日常还是用 pyenv 来安装和管理多个 python 版本。