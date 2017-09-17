---
layout:     post
title:      CHIP-seq作业2--数据下载
subtitle:   zd00572
date:       2017-09-10
author:     zd200572
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
    - 生物信息
    - bioinformatics
    - notes
    - CHIP-seq
---
> step2:读文章拿到测序数据
>
> 本次讲解选取的文章是为了探索PRC1，PCR2这样的蛋白复合物，不是转录因子或者组蛋白的CHIP-seq，请注意区别。
>
> 文章题目
>
> RYBP and Cbx7 define specific biological functions of polycomb complexes in mouse embryonic stem cells
>
> <https://www.ncbi.nlm.nih.gov/pubmed/23273917>
>
> 从文章里面找到数据存放地址如下：
>
> 数据下载：
>
> - <https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE42466>
> - ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByStudy/sra/SRP/SRP017/SRP017311
>
> 作业2
>
> 看文章里的methods部分，把它用到的软件和参数摘抄下来，然后理解GEO/SRA数据库的数据存放形式，把规律和笔记发在论坛上面

1. 数据下载

   ＡＳＣＰ下载，完全利用你的带宽：

   之前看jimmy大神使用shell 脚本下载的，我试着用python脚本搞定了。

   原理是相通的，只不过python还是间接使用shell，大概是多此一举，但我对python最熟了。优点是win下也可用，跨平台。代码周一补上。

    `import os`

    `for  i in range(205, 210):`

    	`print(i)`

    	`cmd = ' ascp -QT -l 100M -k1 -i asperaweb_id_dsa.openssh anonftp@ftp-private.ncbi.nlm.nih.gov:/sra/sra-instant/reads/ByStudy/sra/SRP/SRP017/SRP017311/SRR620' + '%s' % i +'/SRR620' + '%s.sra' % i + ' d:\\'`

    	`print(cmd)`

    	`os.system(cmd)`

   ​

2. 参数

1）bowtie2:two mismatches were allowed within the seed alignment

2)  MACS2:p value cutoff (1 × 10−5).

