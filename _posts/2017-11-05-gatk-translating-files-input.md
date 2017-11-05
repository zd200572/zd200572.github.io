---
layout:     post
title:      GATK软件需要的输入文件是哪些？
subtitle:   zd00572
date:       2017-11-05
author:     zd200572
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
    - 生物信息
    - 软件
    - gatk
    - Notes
---
> [GATK中文社区](https://www.gatk.com.cn)
>
> [gatk-chinese github](https://github.com/gatk-chinese)
>
> [生信技能树](http://www.biotrainee.com)
>
> 这是第二篇：

原文链接：[ What input files does the GATK accept / require? ](https://software.broadinstitute.org/gatk/documentation/article?id=1204)

使用GATK进行的分析通常涉及以下几个输入文件(但不一定是全部) :

- 参考基因组序列
- 测序读取(reads)
- 间隔列表？
- 有序的参考数据

本文介绍了可与GATK一起使用的相应文件格式。

------

### 1. 参考基因组序列

GATK要求参考序列中的单个序列为fasta格式，并且所有的contigs都在同一文件中。GATK要求严格遵守FASTA标准。所有标准的IUPAC碱基都是可以接受的，但请记住，非标准碱基（即非ACGT，如W为例）将被忽略（即在基因组中的位置将被忽略）。 

**一些用户报告说，已在windows文件系统上存储或修改的参考文件存在问题。问题表现为“10”字符（对应编码的换行符）插入序列，导致GATK报错退出。如果您遇到此问题，您将需要重新下载参考文件的有效副本，或自行清理。**

GATK不能使用gzip压缩的fasta文件，因此请确保首先解压缩它们。请参阅[此文](http://www.broadinstitute.org/gatk/guide/article?id=1601) ，了解有关准备GATK使用的fasta参考序列的更多信息。

#### 关于人类基因组参考版本的重要说明

如果您使用的是人类数据，则您的读取必须与一个官方的b3x (例如b36、b37 )或hg1x (例如hg18、hg19)参考序列比对。所使用参考序列中的contigs的名称和顺序必须与官方参考序列规范排序的名称和顺序完全匹配。b3x的参考序列都是由历史上染色体的类型最大到最小，其次是X、Y和MT来定义的；因此顺序是1, 2, 3, ..., 10, 11, 12, ... 20, 21, 22, X, Y, MT。hg1x参考序列的区别在于染色体的名字前面都有“CHR”，chrM出现在头上而不是最后。GATK将检测到contigs错误的排序(例如，按字母顺序排序)并报错。 这种严厉的方法，虽然在技术上是不必要的，但确保了提供给GATK的所有补充数据都正确无误。您可以使用ReorderSam来修复一个与错误排序的参考序列比对的BAM文件。

**我们的最佳实践建议您使用来自GATK资源包的标准GATK参考文件。**

------

### 2. 测序读取

GATK本身支持的序列读取的唯一输入格式是[Sequence Alignment/Map (SAM)] 。有关[SAM/BAM] 格式以及[Samtools](http://samtools.sourceforge.net/) 和[Picard](http://picard.sourceforge.net/)的更多详细信息，请参见 [SAM/BAM]，两个用于处理SAM/BAM文件的互补实用程序。

如果您在本节中找不到需要的信息，请看我们 [关于BAM的常见问题解答](http://www.broadinstitute.org/gatk/guide/article?id=1317)。

如果您使用原始的读取(通常是FASTQ格式)开始您的流程，您需要确保在将这些读取映射到参考序列并生成一个BAM文件时，生成的BAM文件完全符合GATK要求。有关如何完成此操作的详细说明，请参见最佳实践文档。

除了使用SAM格式之外，我们还需要以下附加的约束，以便GATK使用您的文件

：

- 必须是二进制文件 (文件扩展名为`.bam`)。

- 必须对文件进行索引。

- 该文件必须按照参考文件的坐标顺序进行排序 （例如，在您的bam中contig

  的排序必须与您使用的参考序列完全匹配）。

- 文件必须有一个正确的BAM文件头与读取组。每个读取组必须包含平台（PL）和样本（SM）标签。 对于平台，我们当前支持454、ls454、illumina公司、solid、ABI _ solid和CG(所有情况不区分大小写)。

- 文件中的每一个读取必须与一个读组相关联。

下面是一个格式良好的SAM字段头和字段示例 (在@SQ字典中截短了，为了简洁只显示前两条染色体。):

```
@HD     VN:1.0  GO:none SO:coordinate
@SQ     SN:1    LN:249250621    AS:NCBI37       UR:file:/lustre/scratch102/projects/g1k/ref/main_project/human_g1k_v37.fasta    M5:1b22b98cdeb4a9304cb5d48026a85128
@SQ     SN:2    LN:243199373    AS:NCBI37       UR:file:/lustre/scratch102/projects/g1k/ref/main_project/human_g1k_v37.fasta    M5:a0d9851da00400dec1098a9255ac712e
@RG     ID:ERR000162    PL:ILLUMINA     LB:g1k-sc-NA12776-CEU-1 PI:200  DS:SRP000031    SM:NA12776      CN:SC
@RG     ID:ERR000252    PL:ILLUMINA     LB:g1k-sc-NA12776-CEU-1 PI:200  DS:SRP000031    SM:NA12776      CN:SC
@RG     ID:ERR001684    PL:ILLUMINA     LB:g1k-sc-NA12776-CEU-1 PI:200  DS:SRP000031    SM:NA12776      CN:SC
@RG     ID:ERR001685    PL:ILLUMINA     LB:g1k-sc-NA12776-CEU-1 PI:200  DS:SRP000031    SM:NA12776      CN:SC
@PG     ID:GATK TableRecalibration      VN:v2.2.16      CL:Covariates=[ReadGroupCovariate, QualityScoreCovariate, DinucCovariate, CycleCovariate], use_original_quals=true, defau 
t_read_group=DefaultReadGroup, default_platform=Illumina, force_read_group=null, force_platform=null, solid_recal_mode=SET_Q_ZERO, window_size_nqs=5, homopolymer_nback=7, except on_if_no_tile=false, pQ=5, maxQ=40, smoothing=137       UR:file:/lustre/scratch102/projects/g1k/ref/main_project/human_g1k_v37.fasta    M5:b4eb71ee878d3706246b7c1dbef69299
@PG     ID:bwa  VN:0.5.5
ERR001685.4315085       16      1       9997    25      35M     *       0       0       CCGATCTCCCTAACCCTAACCCTAACCCTAACCCT     ?8:C7ACAABBCBAAB?CCAABBEBA@ACEBBB@?     XT:A:U  XN:i:4    X0:i:1  X1:i:0  XM:i:2  XO:i:0  XG:i:0  RG:Z:ERR001685  NM:i:6  MD:Z:0N0N0N0N1A0A28     OQ:Z:>>:>2>>>>>>>>>>>>>>>>>>?>>>>??>???>
ERR001689.1165834       117     1       9997    0       *       =       9997    0       CCGATCTAGGGTTAGGGTTAGGGTTAGGGTTAGGG     >7AA<@@C?@?B?B??>9?B??>A?B???BAB??@     RG:Z:ERR001689    OQ:Z:>:<<8<<<><<><><<>7<>>>?>>??>???????
ERR001689.1165834       185     1       9997    25      35M     =       9997    0       CCGATCTCCCTAACCCTAACCCTAACCCTAACCCT     758A:?>>8?=@@>>?;4<>=??@@==??@?==?8     XT:A:U  XN:i:4    SM:i:25 AM:i:0  X0:i:1  X1:i:0  XM:i:2  XO:i:0  XG:i:0  RG:Z:ERR001689  NM:i:6  MD:Z:0N0N0N0N1A0A28     OQ:Z:;74>7><><><>>>>><:<>>>>>>>>>>>>>>>>
ERR001688.2681347       117     1       9998    0       *       =       9998    0       CGATCTTAGGGTTAGGGTTAGGGTTAGGGTTAGGG     5@BA@A6B???A?B??>B@B??>B@B??>BAB???     RG:Z:ERR001688    OQ:Z:=>>>><4><<?><??????????????????????       
```

#### 关于使用其他排序的bam文件修复的注意事项

GATK要求BAM文件必须按照和参考文件相同的顺序进行排序。不幸的是，许多BAM文件都有按其他顺序排序的头文件 --词典顺序是一种常见的替代。重新排序BAM文件，请使用[ReorderSam](http://picard.sourceforge.net/command-line-overview.shtml#ReorderSam)。

------

### 3. 间隔列表

GATK接受以几种不同格式处理基因组子集的间隔文件。 详细见[FAQs on interval lists](http://www.broadinstitute.org/gatk/guide/article?id=1319) 。

------

### 4. 有序参考序列数据(ROD)文件格式

GATK可以将任意有序参考序列数据(ROD)文件与所有工具的命名tracks关联起来。有些工具需要特定的ROD数据文件进行处理，开发人员可以自由地使用ROD接口开发访问任意数据集的工具。通用ROD系统具有以下语法：

```
-argumentName:name,type file
```

这里的`name`是在GATK工具的名称（如“eval”在VariantEval）， `type`是文件的类型，比如VCF或dbSNP文件，并包含ROD数据文件的路径。

GATK支持几种常见的文件格式读取ROD数据：

- [VCF](http://www.1000genomes.org/wiki/analysis/variant-call-format/) : VCF格式，表示变异位点和基因型调用的推荐格式。GATK将只处理有效的vcf文件；[VCFTools](http://vcftools.sourceforge.net/) 提供了官方的vcf验证器。[这里](http://vcftools.sourceforge.net/VCF-poster.pdf)有一个有用的海报详细介绍了VCF规范。
- UCSC格式的dbSNP : dbSNP格式，UCSC的dbSNP数据库输出
- BED : BED格式，一种用于表示基因组间隔数据的通用格式，用于mask和其他间隔输出。**请注意，bed格式是基于0的，而其他大多数格式都是基于1的。请注意，我们不再支持ped格式。请参阅[这里](http://atgu.mgh.harvard.edu/plinkseq/output.shtml)转换 .ped文件到VCF。**

如果您需要VCF文件的更多信息，请参阅我们的VCF文件常见问题，在[这里](http://www.broadinstitute.org/gatk/guide/article?id=1318)和[这里](http://www.broadinstitute.org/gatk/guide/article?id=1268)。