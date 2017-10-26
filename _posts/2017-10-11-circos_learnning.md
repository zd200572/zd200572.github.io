---
layout:     post
title:      circos学习笔记（一）
subtitle:   zd00572
date:       2017-10-11
author:     zd200572
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
    - 生物信息
    - bioinformatics
    - notes
    - circos
---
**在我的腾讯微云里找到了一个上研究生阶段细菌基因组的测序拼接结果，想画个圈图玩玩，于是找到了circos(基因组圈图的绘制),发现还总是把它与cytoscape(网络可视化)混了，也是醉了，本来以为是一个的，原来是不同的，一个是用perl写的（前者），后者是用java的。**

下面，说一下我的安装过程，就是普通的perl，模块安装，然后解压就好了。我是在Windows下用的，win7 32bit，2G ram,电脑性能较差，不知对较大的文件是否能跑起来。

> 参考了生信技能树论坛上生信媛的帖子：
> [http://www.biotrainee.com/thread-753-1-1.html](http://www.biotrainee.com/thread-753-1-1.html)


1.首先**安装**了**Strawberry Perl**,[http://strawberryperl.com/](http://strawberryperl.com/)
2.然后安装相应的模块：

安装使用**cpan**，就是打开cmd或者powershell,输入cpan，然后install +包名称就好了。

    Config::General
    File::Basename
    File::Spec::Functions
    GD
    GD::Polyline
    Getopt::Long
    IO::File
    List::Util
    Math::Bezier
    Math::BigFloat
    Math::Round
    Math::VecStat
    Memoize
    Params::Validate
    Pod::Usage
    Readonly
    Set::IntSpan
    Regexp::Common
安装了以上包，然后运行发现提示还缺包，同样方法安装了。

**3.下载解压circos**

[http://circos.ca/software/download/circos/](http://circos.ca/software/download/circos/)

然后用7-zip等软件解压到一个目录，如D：\circos\

还可以加入系统环境变量（我的电脑--属性--高级系统设置--环境变量--PATH--添加上路径）

**4.使用示例测试运行**

    D:
    cd Mz\circos-0.69-6\example
    circos etc\-conf circos.conf
    
    cat a.txt | tr -d "^M" > b.txt
    #linux下 win换行符转换，后面报错以为是这个原因，不是的。
**5.测试画个最简单的圈**

使用生信媛的最小配置文件报错，没找到解决方法，在circos官网上找到了一个circos.conf，成功解决。

[http://circos.ca/documentation/tutorials/quick_start/hello_world/](http://circos.ca/documentation/tutorials/quick_start/hello_world/)

    # circos.conf
    
    karyotype = data/karyotype/karyotype.human.txt
    
    <ideogram>
    
    <spacing>
    default = 0.005r
    </spacing>
    
    radius= 0.9r
    thickness = 20p
    fill  = yes
    
    </ideogram>
    
    ################################################################
    # The remaining content is standard and required. It is imported 
    # from default files in the Circos distribution.
    #
    # These should be present in every Circos configuration file and
    # overridden as required. To see the content of these files, 
    # look in etc/ in the Circos distribution.
    
    <image>
    # Included from Circos distribution.
    <<include etc/image.conf>>
    </image>
    
    # RGB/HSV color definitions, color lists, location of fonts, fill patterns.
    # Included from Circos distribution.
    <<include etc/colors_fonts_patterns.conf>>
    
    # Debugging, I/O an dother system parameters
    # Included from Circos distribution.
    <<include etc/housekeeping.conf>>

人家的图片是这样的，
![](http://www.biotrainee.com/data/attachment/forum/201702/01/171719gmazmuggxmy3qhmm.jpg)
我的图片是这样的：
![](http://owxbk335s.bkt.clouddn.com/circos.png)
要哭了，我表示是作者没有给我完整测试数据好不好！有时间用自己的数据跑一遍！





