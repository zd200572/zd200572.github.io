---
layout:     post
title:      (译)flexbar3.0安装笔记
subtitle:   NGS学习笔记
date:       2017-12-22
author:     zd200572
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - NGS质控

---

# 1.源码安装

这是我的弱项，安装以各种报错告终，还好有二进制版本。ps.我曾经为此想要学习从头编译linux或者来个gentoo和arch之类的极客版本玩玩，但是这个难度更大，不过，鉴于我手头的好几台电脑，这个实现还是有希望的。

# 2.二进制安装

## 2.1 首先是我遇到的系统更新cdrom问题

百度一下找到了解决方案：

报错信息：**Media change: please insert the disc labeled**

可以打开文件**/etc/apt/sources.list**文件，注释掉cdrom那一行。

参考自：http://blog.csdn.net/purplegalaxy/article/details/39495033

## 2.2 加入环境变量

解压就不说了，这个加入环境变量比较特别，不是PATH，而是别的：

```sh
export LD_LIBRARY_PATH=/path/FlexbarDir:$LD_LIBRARY_PATH
export PATH="/home/biolinux/biosoft/flexbar-3.0.0-linux::$PATH"
```

运行还是提示找不到命令，于是我又加了一个传统的环境变量。

# 2.3 还是 gcc报错的解决

/usr/lib64/libstdc++.so.6: version `GLIBCXX_3.4.20' not found

原来是系统自带的gcc版本过低了。

升级到4.9就能解决问题

```sh
1 sudo add-apt-repository ppa:ubuntu-toolchain-r/test
2 sudo apt-get update
```

```sh0
3 sudo apt-get upgrade # 这行应该不是必须的。

4 sudo apt-get install gcc-4.9 g++-4.9
5 sudo apt-get install gcc-5 g++-5
```

搞定：

```sh
biolinux@E431[bin] flexbar                             [11:04上午]
flexbar - flexible barcode and adapter removal
==============================================
    flexbar -r reads [-b barcodes] [-a adapters] [options]
    Try 'flexbar --help' for more information.

VERSION
    Last update: March 2017
    flexbar version: 3.0
    SeqAn version: 2.2.0

Available on github.com/seqan/flexbar

Please specify reads input file.

```

我的个人博客：[http://blog.zd200572.com](http://blog.zd200572.com/)和[www.zd200572.com](http://www.zd200572.com/)