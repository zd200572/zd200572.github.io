---
layout:     post
title:      RNAseq实际操作（实战） 
subtitle:   zd00572
date:       2017-07-15
author:     zd200572
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - Bioinformatics
    - Notes
    - 生物信息
---

# RNAseq实际操作（实战） #
首先声明，虽然是实战，但是其实是学习笔记而已，初学，参考了大量大神的博客和帖子,还有大神引用的大牛的帖子,参考列表见最后。

## 1、软件安装 ##
### 1.1 硬件系统情况

系统：BioLinux8（ubuntu14.04.2-x64）

电脑配置：

Lenovo-ThinkPad-E431

    CPU系列 英特尔 酷睿i3 3代系列
    CPU型号 Intel 酷睿i3 3120M
    CPU主频 2.5GHz
    总线规格 DMI 5 GT/s
    三级缓存 3MB
    核心架构 Ivy Bridge
    核心/线程数 双核心/四线程
    制程工艺 22nm
    内存容量 12GB（4GB×1 + 8GB×1）

### 1.2 软件安装

有简单的不必去重新编译代码了，bioconda几个命令解决，可能软件依赖会有点问题。

1）Miniconda安装

 `wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh`

`bash Miniconda3-latest-Linux-x86_64.sh`

一路Enter搞定

2）sratoolkit

`conda install -c jfear sratoolkit  `

3）fastqc

`conda install fastqc`

发现fastqc是BioLinux自带的，执行这个命令只是升级了java

4）**hisat2**

`conda install hisat2`

`hisat2 -h  #测试`

5）samtools

`conda install samtools`
`samtools`

''#samtools也是自带的，执行这个命令会说依赖冲突，因为我的conda是Python3.6版，有点新，不兼容正常。

6）htseq-count

`conda install -c bioconda htseq` 

’#测试

`python`

`>>> import HTSeq`

7）R 

BioLinux自带了，升级一下到3.4.1

`sudo add-apt-repository ppa:marutter/rrutter` 

`sudo apt-get update ‘`

`sudo apt-get install r-base r-base-dev` 

8）rstudio

`conda ``install` `rstudio`

`rstudio`

## 2、读文章拿到测序数据 ##

直接拿jimmy的脚本修改得来的。仔细分析项目数据后，得到要下载的数据是SRR3589958-62

这个脚本包含了下载数据，sra格式转化为fastq，fastqc对转化的数据进行分析，代码如下：

`for ((i=958;i<=958;i++)) ;do wget ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByStudy/sra/SRP/SRP075/SRP075747/SRR3589$i/SRR3589$i.sra;done`

`ls *sra |while read id; do fastq-dump --gzip --split-3 $id;done`

`ls *fastq |while read id; do fastqc $id;done`

## 3、了解fastq测序数据（fastqc质量控制学习） ##
>
1.fastqc
`zcat SRR3589956_1.fastq.gz | fastqc -t 4 stdin
fastqc SRR3589956_1.fastq.gz`
`#t 线程，每个250M内存`

2.multiQC

`conda install multiqcmultiqc `
`# 先获取QC结果`

`ls *gz | while read id; do fastqc -t 4 $id; done`

`# multiqc`

`multiqc *fastqc.zip --pdf`

![](http://osnq2ssd7.bkt.clouddn.com/rnaseq1.png)

![](http://osnq2ssd7.bkt.clouddn.com/rnaseq2.jpg)

![](http://osnq2ssd7.bkt.clouddn.com/rnaseq3.png)
## 4、了解参考基因组及基因注释 ##
1）下载参考基因组
`wget http://hgdownload.soe.ucsc.edu/goldenPath/hg19/bigZips/chromFa.tar.gz` #wget 下载或者其他工具下载

`tar -zvf chromFa.tar.gz`

`cat *.fa > hg19.fa`

`rm chr*`

2）下载基因组注释gtf文件

` wget ftp://ftp.sanger.ac.uk/pub/gencode/Gencode_human/release_26/GRCh37_mapping/gencode.v26lift37.annotation.gtf.gz]ftp://ftp.sanger.ac.uk/pub/genco ... 7.annotation.gtf.gz`

3)下载IGV(Integrative Genomics Viewer)

下载地址为：[ http://software.broadinstitute.org/software/igv/download]( http://software.broadinstitute.org/software/igv/download)

4)genome -> Load Genome From Files加载之前得到基因组文件

5)Tool -> Run igvtools，进行排序

6)加载gff基因注释文件，File -> Load From Files

7)可视化分析
同样推荐阅读生信宝典公众号文章。

[https://mp.weixin.qq.com/s/Q7pqycmQH58xU6hw_LECWA](https://mp.weixin.qq.com/s/Q7pqycmQH58xU6hw_LECWA)


>
1、[http://www.biotrainee.com/forum.php?mod=viewthread&tid=1750#lastpost](http://www.biotrainee.com/forum.php?mod=viewthread&tid=1750#lastpost)#jimmy的导航贴
>
转录组入门(1)：计算机资源的准备
最好是有mac或者linux系统，8G+的内存，500G的存储即可。

如果你是Windows，那么安装必须安装 git,notepad++,everything，还有虚拟机，在虚拟机里面安装linux，最好是ubuntu。

需要安装的软件包括 sratoolkit,fastqc,hisats,samtools,htseq-count,R,Rstudio 
>
软件安装的代码，在生信技能树公众号后台回复老司机即可拿到。
进阶作业，每个软件都收集一个中文教程链接，并自己阅读，发在论坛里面。
>
目前有5份优秀作业，请大家学习：
>
[转录组（一）](http://www.biotrainee.com/thread-1800-1-1.html)作业  ( HOPTOP )  
>
[转录组入门(1)](http://www.biotrainee.com/thread-1796-1-1.html)-作业  (青山屋主)
>
[转录组入门（1）](http://www.biotrainee.com/thread-1810-1-1.html)Mac上软件准备作业 
>
[PANDA姐的转录组入门(1)](http://www.biotrainee.com/thread-1847-1-1.html)：计算机资源的准备 
>
[转录组作业（一）](http://www.biotrainee.com/thread-1850-1-1.html)：来自零基础的小白
>
[转录组入门(2)：读文章拿到测序数据](http://www.biotrainee.com/thread-1743-1-1.html)
>
本系列课程学习的文章是：AKAP95 regulates splicing through scaffolding RNAs and RNA processing factors. Nat Commun 2016 Nov 8;7:13347. PMID: 27824034 很容易在文章里面找到数据地址GSE81916 这样就可以下载sra文件
>
作业，看文章里的methods部分，把它用到的软件和参数摘抄下来，然后理解GEO/SRA数据库的数据存放形式，把规律和笔记发在论坛上面！优秀作业如下：
>
[转录组入门（二）](http://www.biotrainee.com/thread-1829-1-1.html)作业 New(HOPTOP)
>
[转录组入门(2)](http://www.biotrainee.com/thread-1884-1-1.html)-作业(青山屋主)
>
[PANDA姐的转录组入门(2)：读文章拿到测序数据](http://www.biotrainee.com/thread-1853-1-1.html)
>
转录组入门(3)：了解fastq测序数据
>
需要用安装好的sratoolkit把sra文件转换为fastq格式的测序文件，并且用fastqc软件测试测序文件的质量！
作业，理解测序reads，GC含量，质量值，接头，index，fastqc的全部报告，搜索中文教程，并发在论坛上面。
目前优秀作业有：
>
[转录组（三）](http://www.biotrainee.com/thread-1831-1-1.html)：作业（HOPTOP）
>
[转录组入门(3)](http://www.biotrainee.com/thread-1885-1-1.html)-作业（青山屋主）
>
[PANDA姐的转录组入门(3)](http://www.biotrainee.com/thread-1853-1-1.html):了解fastq测序数据
>
转录组入门(4)：了解参考基因组及基因注释
>
在UCSC下载hg19参考基因组，我博客有详细说明，从gencode数据库下载基因注释文件，并且用IGV去查看你感兴趣的基因的结构，比如TP53,KRAS,EGFR等等。
>
作业，截图几个基因的IGV可视化结构！还可以下载ENSEMBL，NCBI的gtf，也导入IGV看看，截图基因结构。了解IGV常识。
目前优秀作业是：
>
hoptop的：[转录组作业（四）](http://www.biotrainee.com/thread-1835-1-1.html) 
>
转录组入门(5)： 序列比对
>
比对软件很多，首先大家去收集一下，因为我们是带大家入门，请统一用hisat2，并且搞懂它的用法。
>
直接去hisat2的主页下载index文件即可，然后把fastq格式的reads比对上去得到sam文件。
>
接着用samtools把它转为bam文件，并且排序(注意N和P两种排序区别)索引好，载入IGV，再截图几个基因看看！
>
顺便对bam文件进行简单QC，参考直播我的基因组系列。
目前优秀作业是：
>
[转录组入门(5)](http://www.biotrainee.com/thread-1870-1-1.html)： 序列比对（HOPTOP）
>
转录组入门(6)： reads计数
>
实现这个功能的软件也很多，还是烦请大家先自己搜索几个教程，入门请统一用htseq-count，对每个样本都会输出一个表达量文件。
>
需要用脚本合并所有的样本为表达矩阵。参考：生信编程直播第四题：多个同样的行列式文件合并起来
>
对这个表达矩阵可以自己简单在excel或者R里面摸索，求平均值，方差。
看看一些生物学意义特殊的基因表现如何，比如GAPDH,β-ACTIN等等。
>
转录组入门(7)： 差异基因分析
>
这个步骤推荐在R里面做，载入表达矩阵，然后设置好分组信息，统一用DEseq2进行差异分析，当然也可以走走edgeR或者limma的voom流程。
基本任务是得到差异分析结果，进阶任务是比较多个差异分析结果的异同点。
>
转录组入门(8)： 差异基因结果注释
>
我们统一选择p<0.05而且abs(logFC)大于一个与众的基因为显著差异表达基因集，对这个基因集用R包做KEGG/GO超几何分布检验分析。
然后把表达矩阵和分组信息分别作出cls和gct文件，导入到GSEA软件分析。
>
基本任务是完成这个分析。
>
最后，把同样的代码实践与其它几篇转录组文章，并且把代码和分析结果发在论坛上面；
>
http://biotrainee.com/jmzeng/RNA ... E81916-two-group.sh
>
我以前在博客写过的
http://www.bio-info-trainee.com/2218.html
比如可以来一个实战：
生信技能树»生信技能树›互动作业›项目实战›mRNA-seq数据分析实战