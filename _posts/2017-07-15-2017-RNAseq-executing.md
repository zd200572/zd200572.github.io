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

 ``wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh`

`bash Miniconda3-latest-Linux-x86_64.sh`

一路Enter搞定

2）sratoolkit

conda install -c jfear sratoolkit  

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
>>>`import HTSeq`

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

`for ((i=958;i<=958;i++)) ;do wget ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByStudy/sra/SRP/SRP075/SRP075747/SRR3589$i/SRR3589$i.sra;done

ls *sra |while read id; do fastq-dump --gzip --split-3 $id;done

ls *fastq |while read id; do fastqc $id;done`



## 3、人生要耐得住寂寞（大全集） ##
感动。
## 4、云计算与生活 ##

讲作和生活。

## 5、秦始皇 ##
这是本历史小不要像

## 6、互联网+ ##

感觉这本了，算是复习吧。

## 7、​帝王那些事 ##

这本书应该算而已。

## 8、那时汉朝 ##

讲的是汉朝者，虽远必诛！

## 9、计算机硬盘维修与数据恢复高手 ##

简单少收获。

## 10、第一本Docker书 ##

是Docker己的程序。

