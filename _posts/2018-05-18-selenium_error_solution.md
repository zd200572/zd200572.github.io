---
layout:     post
title:      selenium模块报错的解决
subtitle:   python学习笔记
date:       2018-05-18
author:     zd200572
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - python

---

selenium是一个控制浏览器的模块，66的，挺酷的感觉。我在《python编程快速上手--让繁琐工作自动化（Automate the Boring Stuff with Python）》中读到了这个模块，想试试，却发现问题是不管用哪个浏览器，都会报类似的错误：

> selenium.common.exceptions.WebDriverException: Message: 'geckodriver' executable needs to be in PATH. 

在网上搜了个解决方案是下载这个driver，然后把驱动所在路径放在PATH中（Windows），经过实践发现没有效果，于是继续查解决方案，终于在知乎上找到了：

> https://www.zhihu.com/question/49568096
>
> 1、下载geckodriver.exe：
>
> 下载地址：https://github.com/mozilla/geckodriver/releases请根据系统版本选择下载；（如Windows 64位系统）
>
> 2、下载解压后将getckodriver.exe复制到Firefox的安装目录下，如（C:\Program Files\Mozilla Firefox），并在环境变量Path中添加路径：
>
> C:\Program Files\Mozilla Firefox；重启cmd或IDLE再次运行代码即可**

然后，就可以愉快地玩耍了，继续学习啦！