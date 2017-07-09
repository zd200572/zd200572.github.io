---
layout:     post
title:      RNA-seq分析-学习笔记
subtitle:   zd00572
date:       2017-07-09
author:     zd200572
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - 生信
    - Notes
    - Bioinformatics
---

# RNA-seq分析-学习笔记

从南京图书馆借了本《生物信息学最佳实践》（冉隆科. 生物信息学最佳实践[M]. 科学出版社, 2016.），前几章的笔记记在了纸质笔记本上，感觉还是电子版的可以更便携，刚好一本笔记本记完了，剩下的简略的笔记就记在这里了。

## 一、分析流程(pipeline)

测序(.fastq)——Bowtie/TopHat(.fa)(read alignment)——Cufflinks(.gtf)(transcript compilation)——cuffmerge(gene identification)——Cuffdiff(differential expression)——CummRbund(visualization)

###  1、数据准备

###  2、软件准备

####    a、TopHat（短读段映射）

####    b、Bowtie（一个超快的短读段比对工具）

####    c、Cufflinks（转录组装配）

####    d、CummeRbund（R的bioconductor包进行差异可视化表达）

####    e、Samtools(读段识别工具)

###  3、分析过程

####    a、构建索引文件

bowtie2-build genome-fasta-file index-name

####    b、比对

tophat [options] index-base reads1 reads2

-p:CPU线程数

--solesa-quals

--library-type:链特异性library type（illumia fr-untrusted）

DrZv9.66 #参考基因索引文件前辍

#### d、转录组重建

cufflinks [options]* aligned_reads.sam/bam

-g :gff格式注释文件

-b:较正算法

-u:初步评估

#### e、合并装配后的转录本文件

cuffmerge -p 4 -g annotation/DrZv9.66_chr12.gtf -s genome/Zv9.fa assemblies.txt

#### f、识别新的转录本

上步文本中每行包含一个注释字段（class_node）

#### g、差异表达分析

cuffdiff

-L:不同样品条件

-T：不同时间序列条件

#### h、使用cummeRbund包进行差异表达分析

'>library(cummeRbund)#载入包

cuff = readCufflinks('diff_out')#导入cuffdiff结果文件夹中diff_out

csDensity(genes(cuff))#表达值分布

csScatter(genes(cuff), ZV9_2cells', 'ZV9-6h')#散点图

csScatterMatrix(genes(cuff))#检查单个密度和与之配对的散点图

csVolcanoMatrix(genes(cuff)), 'ZV9_2cells', 'ZV9-6h')#火山图

gene_diff_data=diffData(genes(cuff))#基因水平的表达数据

nrow(gene_diff_data)#统计总的表达基因数

sig_gene_data = subset(gene_diff_data, (significant =='yes'))#显著表达差异的基因数

nrow(sig_gene_data)

write.table(sig_gene_data, 'sig_diff_genes.txt', sep = '\t', row.names=FALSE, quote =F)#输出差异到文件中

'

