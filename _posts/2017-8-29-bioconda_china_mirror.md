---
layout:     post
title:      七夕刚过，bioconda中国镜像来临
subtitle:   zd00572
date:       2017-08-29
author:     zd200572
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
    - 健康
    - 互联网+
    - 医疗
    - 大数据
---
**昨天，偶然发现：**

8月22号，让生信小伙伴日顾夜盼的bioconda中国镜像已经在清华tuna镜像源的一个服务器上建成了，感谢那个去呐喊的小伙伴@hyacz。
镜像地址：
[https://nanomirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/](https://nanomirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/)
一直一来，小伙伴们倍受bioconda服务器在国外，没有国内镜像，下载软件缓慢，不时报错的煎熬。这个镜像的到来将为我们解决这个问题。
下面介绍一下镜像的使用方法：

    conda config --add channels https://nanomirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/
    conda config --set show_channel_urls yes
进行一下速度对比，公司百兆电信宽带条件下，以安装bwa软件为例：

![](http://upload-images.jianshu.io/upload_images/6644753-4b0071424d79afca.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

不使用镜像，平均速度169.09KB/s，还是在网络较好的情况下，而且下载大软件容易中断。
![](http://upload-images.jianshu.io/upload_images/6644753-aa03c89f382ea038.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
使用镜像情况，平均速度已经是1.86MB/s，整整提高了十倍，虽然可能还没有进入官方源，有个警告，但是不影响使用。我们可以把更多的时间用在分析数据而不是折腾软件上。

**怎么样，给力吧？快点上车吧！**


