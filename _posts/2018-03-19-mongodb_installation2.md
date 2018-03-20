---
layout:     post
title:      mongodb安装笔记（windows、Mac 10.9和linux）
subtitle:   微生物学习笔记
date:       2018-02-09
author:     zd200572
header-img: img/post-bg-alitrip.jpg
catalog: true
tags:
    - mongodb

---

由于拥有好几台电脑，折腾便成了我的乐趣，从windows，Mac OSX 10.9到10.10、10.11，linux deepin 15.4，kali,以及树阿莓派的raspbian，服务器的ubuntu server都是我的折腾对象，这也部分反应了物欲横流的我啊！但是这样也多了解了点不同操作系统的差异，可专注性还是不好啊！看到每个论坛的资深发烧友都有收藏癖，像51专门网的大哥们每个人人手几台thinkpad小黑，chromebook群里有人几台chromebook，资深果粉逢出必买，数码之家的网友一堆电子古董，486什么的各种收藏，龙芯吧的小伙伴们拥有好几台龙芯，电纸书爱好者的好几个电纸书。。。说了这么多，我好像暴露了好多信息。

下面是我的mongodb折腾经验，linux操作系统，比较简单，一般都已经编译好的包，直接apt install mongodb或者yum 什么的，连树莓派都可以这样搞定，只不过版本偏低，想追求高的，添加mongodb软件源即可。

mac操作系统，10.11的，上面已经说过了，用mongodb去装个低版本的，至于古董级别的，就从官网下个这个系统那个时间的版本，不得不吐槽，mac的系统兼容性实在太差，注定难以成为一个大众的操作系统，不能成为生产中可靠的依赖。

win版本也比较简单，只不过解压然后添加环境变量就好了，或者是使用安装版本。

至于开机启动，win是把它注册为服务，linux是添加rc.d，mac是添加plist。针对于gui管理工具的使用，如果本地使用没问题，如果是像我一样云服务器使用，就要修改/etc/mongodb/config.conf中的bind的ip为你的ip或者0.0.0.0即可，好像这样有点不安全的。

一直好奇，这是不是应该叫芒果数据库，听着好好玩，文档数据库。


**我的个人博客 **：[http://jiawen.zd200572.com](http://blog.zd200572.com/)和[www.zd200572.com](http://www.zd200572.com/)



