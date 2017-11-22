---
layout:     post
title:      R语言包安装笔记
subtitle:   Y叔包yyplot艰辛安装
date:       2017-11-21
author:     zd200572
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - R
---

在Y叔的微信公众号看到了一个好久就想用的功能包，可以用来看**文章发表趋势**的，一直心痒，尝试了n次以后，终于安装成功了。这过程中有几个重要的点，需要记录下来：

# 1.github包的安装

在百度上找的代码已经过时了，虽然仅仅是符号的差别，但是还是挺不方便的，把我找到的代码放在这。

```R
install.packages("devtools")

library(devtools)

install_github("GuangchuangYu/yyplot")
```

在百度上搜到的最后一步是以‘，’分隔的，包提示已经过时了，新的表示方法更加直观呀！另外就是缺什么包安什么包了，什么bioconductor, CRAN等。

bioconductor中科大源的使用：

```R
source("https://bioconductor.org/biocLite.R")

options(BioC_mirror="http://mirrors.ustc.edu.cn/bioc/") 

biocLite("magick")
```

听讲座得知R语言的一个开发者就是学生物的，开发完R就做了Bioconductor，厉害呀，膜拜！

# 2.Windows系统下的安装路径问题

在win下安装github包不知道为什么报错了说找不到命令（'G:\Program ' 不是内部或外部命令,也不是可运行的程序），我观察发现路径中有个空格，可能导致不识别，于是重新安装了R到其他不带空格的路径得以解决。

# 3.yyplot的试用

终于到了Y叔的yyplot登场了，测试一下，画了个研究生导师的文章发表趋势：

![](http://owxbk335s.bkt.clouddn.com/jian%20he.png)

应该是有重名的，还是挺棒的，这么简单的包，赶紧用起来！

```R
#用作者的示例加上我研究生阶段的课题
library(yyplot)

term <- c('"thiobencarb"')

pm <- pubmed_trend(term, year=2001:2017)

plot(pm)
```

![](http://owxbk335s.bkt.clouddn.com/thiobencarb.png)

课题不是怎么热哈！

**版权属于作者（ *Y叔* [biobabble](https://mp.weixin.qq.com/s?src=11&timestamp=1511326740&ver=529&signature=r3*GLbWm4nQzzJgEfW8am83nHCJXV2DWP0p6i6ZiPWATEXHNm5LQuWetgR6Ir0t0GH9yuGX4hq6vH5C-By9gY*o5QJx0Wie6bGDwF-IG9m-d2DlQfnCSHDnFsoq19Cw*&new=1##)），我只是个使用者，为了尊重作者，放上他的微信公众号二维码。**

![](http://owxbk335s.bkt.clouddn.com/biobable)



我的个人博客：[http://blog.zd200572.com](http://blog.zd200572.com/)和[www.zd200572.com](http://www.zd200572.com/)