---
layout:     post
title:      omictools的HLA分型软件爬取
subtitle:   rvest学习笔记
date:       2018-01-14
author:     zd200572
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - rvest

---

> 某天在生信技能树变异查找群里看到有个来自台湾的哥们要在合肥举办讨论R语言爬虫的讲座，引起了我的兴趣，刚好最近在学习HLA分型方面的内容，在omictools网站上测试一下。

# 1.工具名称爬取

首先安装上rvest的包，直接安装就可以了。然后，加载包，读取网址。代码参考自知乎教程：https://zhuanlan.zhihu.com/p/22940722

检查一下工具名称的标签，

`<span class="tool-section-grid-item-content-title-long">POLYSOLVER</span>`

```R
install.packages("rvest") \
library(rvest) \
web<-read_html("https://omictools.com/hla-typing-category",encoding="UTF-8") \
position<-web %>% html_nodes("span.tool-section-grid-item-content-title-long")%>% html_text() \
> position \
 [1] "POLYSOLVER"               "PyHLA"                    "HLA-MA"     \             
 [4] "HLA-PRG"                  "Hapl-o-Mat"               "Saddlebags"        \      
 [7] "Graphtyper"               "HLAreporter"              "HLAscan"          \       
[10] "HLA-VBSeq"                "ATHLATES"                 "SAF"             \        
[13] "OptiType"                 "HLATyphon"                "PHLAT"            \       
[16] "Assign"                   "Omixon Target HLA Typing" "HLAminer"          \      
[19] "HLA Completion"           "HLAforest"                "Gyper"   \
```

好，这么简单的代码，工具名称就得到了，好像比python的BeautifulSoup还要简单点，各有优势啦。

# 2.代码网址爬取

工具网址在这个标签里，虽然比较隐藏，还是发现了。

`<a href="/polymorphic-loci-resolver-tool" class="js-tool-card-link" title="POLYmorphic loci reSOLVER - POLYSOLVER">`

然后就是和上面一样，选择一下就好了。

```R
position<-web %>% html_nodes("h2.tool-section-grid-item-content-title") %>% html_nodes("a.js-tool-card-link" )%>% html_attr("href") \
> position \
 [1] "/polymorphic-loci-resolver-tool" "/pyhla-tool"                 \   
 [3] "/hla-ma-tool"                    "/hla-prg-tool"                \  
 [5] "/hapl-o-mat-tool"                "/saddlebags-tool"              \ 
 [7] "/graphtyper-tool"                "/hlareporter-tool"             \ 
 [9] "/hlascan-tool"                   "/hla-vbseq-tool"                \
[11] "/athlates-tool"                  "/second-allele-finder-tool"     \
[13] "/optitype-tool"                  "/hlatyphon-tool"                \
[15] "/phlat-tool"                     "/assign-tool"                   \
[17] "/omixon-target-hla-typing-tool"  "/hlaminer-tool"                 \
[19] "/hla-completion-tool"            "/hlaforest-tool"                \
[21] "/graph-genotyper-tool"          \
```

表示so easy嘛，这样就获得了，下面可以继续爬取各个工具的情况了。网址的组成就是https://omictools.com/polymorphic-loci-resolver-tool等等，很清楚明了。

由于对R不够熟悉，就用python了，反正都是完成相应的任务，条条大路通罗马。

我的个人博客：[http://blog.zd200572.com](http://blog.zd200572.com/)和[www.zd200572.com](http://www.zd200572.com/)



