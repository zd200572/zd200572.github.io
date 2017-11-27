---
layout:     post
title:      使用谷歌云计算引擎
subtitle:   建站、搭梯，妥妥地
date:       2017-11-24
author:     zd200572
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - 服务器
---

在生信技能树的微信公众号看到了一个搭梯的教程，挺好奇的，也测试一下：

# 1.开通谷歌云服务器帐号

大概就是注册个谷歌帐号，然后开通这项服务。这个百度了个教程，参考了一下：

> http://bbs.feng.com/read-htm-tid-10722506.html

# 2.安装相关工具

就依照jimmy的指示操作就可以了。值得注意的一点是安装完会出现server IP为0.0.0.0的情况，要改为服务器的IP，对了上面设置的时候要申请独立IP。

其实，大部分操作没有什么难度，只要填好就行了，有一个问题是设置防火墙的时候设置一下端口tcp:8989就可以了，我把出站和入站都设置了，估计只入站就可以。

# 3.上个网站

虽然单核0.6G ram的服务器，但是单这样挂着也挺浪费，挂个网站，上个docker、Rstudio server都可以。就按jimmy的另一篇推文搞了一下，挂了个开源网站。代码如下：

```sh
sudo apt-get install apache2 mysql-server mysql-client php php-gd php5-mysql
#这中间要设置个密码，记好了就好。
#当然，还要设置数据库，我的那个网站开源程序可以自己建数据库，就没有做这个。
```

# 4.安装必备的库(docker用？)

```sh
sudo apt-get -y install libcurl4-gnutls-dev
sudo apt-get -y install libxml2-dev
sudo apt-get -y install libssl-dev
sudo apt-get -y install  libmariadb-client-lgpl-dev
```

# 5.安装R相关

```sh
sudo apt-get update
sudo add-apt-repository ppa:marutter/rrutter
sudo apt-get update
sudo apt-get install r-base-core 
R --version
sudo su - \
-c "R -e \"install.packages( c('RSQLite','shiny','devtools','RMySQL'), repos='https://cran.rstudio.com/')\""
到这里内存报错进行不下去了，600M内存是太小了。
```

我的个人博客：[http://blog.zd200572.com](http://blog.zd200572.com/)和[www.zd200572.com](http://www.zd200572.com/)