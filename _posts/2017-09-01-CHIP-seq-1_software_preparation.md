---
layout:     post
title:      CHIP-seq作业1
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
> step1:计算机资源的准备
>
> 这个跟转录组对计算资源的要求是大同小异的，最好是有mac或者linux系统，8G+的内存，500G的存储即可。
>
> - 如果你是Windows，那么安装必须安装 git,notepad++,everything，还有虚拟机，在虚拟机里面安装linux，最好是ubuntu。
> - 如果本身就是mac或者linux，那么很简单了，安装好wget吧
>
> 需要安装的各种ChIP-seq软件包括 sratoolkit,fastqc,bowtie2,samtools,htseq-count,bedtools,macs2,HOMER,R,Rstudio 
>
> 软件安装的代码，在生信技能树公众号后台回复老司机即可拿到。
>
> 如果呀详细了解计算机配置清单，软件安装等，请查看我们[公众号推文](http://mp.weixin.qq.com/s/e-m8edpa4G-uqZxY4affPA)
>
> 作业1
>
> 安装好软件，下载软件的说明书，整理它们的官网链接。

# 1.软件安装

我表示我是conda党，虽然总有一颗玩玩LFS和Gentoo的心，无奈水平太菜，还有自己有点懒，另外那错误实在是令人无语（我曾经买过一台龙芯2Ｆ 7寸小本，性能是十年前的所以不表，但是由于龙芯生态还不完善，所以源码编译软件各种报错，虽然一直想来个ＬＦＳ，可是水平不够，内核就编不出，所以直到前几天坏了还在尝试。。。至于最近还冒出想要买台龙芯3Ａ3000学习生物信息的念头，看了看大部分软件都是ＢＺ2，木有源码，也就只是想想了。ＬＩＮＵＳ说的对，对于普通人暂时就用生态最好的Ｘ86了，说了好多废话。）。所以，大牛们已为我们做了如此给力的包管理系统，不用浪费呀！我的原则是能用conda等包管理的用之，二进制次之，源码是最后的选择。

系统环境是ＯＳＸ 10.11.5(用的是之前装了很久的黑苹果，最近用优盘引导感觉挺好用的，就用一下。)

`conda install sratools fastqc bowtie2 samtools htseq bedtools macs2  r-base r-base-dev rstudio`

`＃以上代码解决问题，配上清华源，速度杠杠的，爽歪歪呀！`

HOMER软件是个坑，conda大法配合手动安装搞定

`conda install wget samtools r-essentials bioconductor-deseq2 bioconductor-edger`

`＃conda安装依赖，官网推荐`

`wget http://homer.ucsd.edu/homer/configureHomer.pl`

`＃下载脚本`

`mkdir biosoft && mkdir biosoft/homer && mv Downloads/configureHomer.pl biosoft/homer`
`cd biosoft/homer`

`perl configureHomer.pl  -install`

`#安装之，中途两个警告，试了下可以正常运行`

`export PATH="/Users/zd200572/biosofts/homer/bin:$PATH"`

`＃添加到系统变量`

2.官网链接、软件说明书

1)homer

官网：http://homer.ucsd.edu/homer/

说明书：http://homer.ucsd.edu/homer/basicTutorial/index.html

2)sratoolkit

 官网：https://trace.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=software

说明书：https://trace.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=toolkit_doc

3) fastqc

 官网：http://www.bioinformatics.babraham.ac.uk/projects/fastqc/

说明书：http://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/

4) bowtie2

 官网：http://bowtie-bio.sourceforge.net/bowtie2/index.shtml

说明书：http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml

5) samtools

 官网：http://www.htslib.org

说明书：http://www.htslib.org/doc/#manual-pages

6) htseq

 官网：http://htseq.readthedocs.io/en/release_0.9.1/

说明书：http://htseq.readthedocs.io/en/release_0.9.1/

7) bedtools

 官网：http://bedtools.readthedocs.io/en/latest/

说明书：http://bedtools.readthedocs.io/en/latest/

 8)macs2

 官网：https://github.com/taoliu/MACS/

说明书：https://github.com/taoliu/MACS/

  9)r-base r-base-dev

 官网：https://www.r-project.org

说明书：https://cran.r-project.org/manuals.html

10) rstudio

 官网：http://www.rstudio.com

说明书：https://support.rstudio.com/hc/en-us