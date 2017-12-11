---
layout:     post
title:      找变异流程之snp_call
subtitle:   WES学习之路
date:       2017-12-08
author:     zd200572
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - WES
---

> ## 参考了许多WES的流程之后，终于学会了几个找变异软件的使用，记在这里备忘一下。学习不可囫囵吞枣，我还是把软件的各个参数理解下，也充实下内容，避免只有代码的尴尬。

# 1、找变异的前处理

这里主要是对bam文件进行排序，不知道用samtools和picard的差别在哪，但是，02样本用picard会报错的。

对 mapping 得到的 bam 文件做完 Fix Mate Information、Sort 和 mark duplicates 处理后， 就可以进入 GATK 流程了。

 BWA 有时会产生不正常的 flag 信息，在进行其它分析前最好先整理 reads 的 mate 信息以及 flags。

SortSam 并没有依据 Mate 信息进行过滤，MarkDuplicates 如果仅仅是标记重复而不移除重复时，不会对 mate 信息产生影响，当时觉得 FixMateInformation 只要在用 GATK 分析之前运行了就可以 (GATK 默认会依据 mate 信息对数据进行过滤)。

如果 MarkDuplicates 这步把重复去掉，则会对 mate 信息产生影响，可以考虑在这步之后加上 FixMateInformation。

```sh
picard SortSam SORT_ORDER=coordinate INPUT= Illumina_B1702-sorted.dedup.add.bam OUTPUT= Illumina_B1702.add.sorted.bam
# samtools index Illumina_B1702-sorted.bam 这个也能实现
echo MarkDuplicates
java -Xmx9g -jar ~/miniconda3/share/picard-2.14.1-0/picard.jar MarkDuplicates CREATE_INDEX=true REMOVE_DUPLICATES=True ASSUME_SORTED=True VALIDATION_STRINGENCY=LENIENT METRICS_FILE=/dev/null INPUT=Illumina_B1702-sorted.bam OUTPUT=Illumina_B1702-sorted.dedup.bam TMP_DIR=/media/biolinux/LENOVO_imcdul/WEA/tmp

echo FixMateInformation
java -Xmx9g -jar ~/miniconda3/share/picard-2.14.1-0/picard.jar FixMateInformation SO=coordinate VALIDATION_STRINGENCY=LENIENT CREATE_INDEX=true INPUT=Illumina_B1702-sorted.bam OUTPUT=Illumina_B1702-sorted.mate.bam TMP_DIR=/media/biolinux/LENOVO_imcdul/WEA/tmp
```

# 2.freebayes

Boston College Biology一个团队开发的，介绍少的可怜，翻译一下文档：

FreeBayes是一个贝叶斯遗传变异的检测器，发现短读顺序比对的小多态性，特别是SNPs（单核苷酸多态性），INDELS（插入和删除），MNPs（多单核苷酸多态性），和复杂的事（复合插入和替换事件）。

参数挺少的，估计默认参数就挺好的。

```sh
echo freebayes
nohup freebayes -f ../../../hg38/hg38.fa Illumina_B1702.sort.bam > Illumina_B1702_freebayes.vcf &
```

-C ，默认值为2，即变异位点处至少有两个和参考碱基不同，才会考虑是snp位点。

-F 默认为0.2 ,即至少有20%的碱基和参考碱基不同才能被call出。假如某位点深度为100，但是只有10个碱基和参考序列不同，是不会被call出的。

# 3.bcftools

samtools还有个非常重要的命令mpileup，以前为pileup。该命令用于生成bcf文件，再使用bcftools进行SNP和Indel的分析。bcftools是samtool中附带的软件，在samtools的安装文件夹中可以找到。

最常用的参数有2：

 -f 来输入有索引文件的fasta参考序列； -g 输出到bcf格式。

不使用-u或-g参数时，则不生成二进制的bcf文件，而生成一个文本文件(输出到标准输出)。该文本文件统计了参考序列中每个碱基位点的比对情况；该文件每一行代表了参考序列中某一个碱基位点的比对结果。

```sh
Usage: samtools mpileup [-EBug] [-C capQcoef] [-r reg] [-f in.fa] [-l list] [-M capMapQ] [-Q minBaseQ] [-q minMapQ] in.bam [in2.bam [...]]
echo bcftools
nohup samtools mpileup -ugf /media/biolinux/LENOVO_imcdul/hg38/hg38.fa  Illumina_B1702-sorted.bam  |bcftools call -vmO z -o \ Illumina_B1702.bcftools.vcf.gz &
```

# 4.varscan

VarScan2是华盛顿大学开发的一款多用途的call变异工具。可用于种系细胞、体细胞（SNV/INDEL/CNV/）(CNV不建议用，据说是别人提供的脚本，漏洞百出)、de Novo Mutations(trios))等。

VarScan2使用各种过滤方法，以得到各位点在样品中的基因型，并计算各等位基因的read 频率。此工具只支持两种等位基因的基因型。通过比较两个样品在该位点各等位基因的read 频率，并通过fisher’s检验得到差异显著性水平p 值。VarScan2工具将突变位点分为三种突变状态：somatic 突变、germline 突变、LOH 突变；并从三种状态的位点，得到置信位点。

生成1个mpileup文件（官方文档强烈推荐）

samtools  mpileup -q 1  -d 30000  -L 30000 -f ucsc.hg19.fasta  normal.bamtumor.bam  >  normal.tumor.mpileup

 参数说明：-q 1表示跳过比对的mapQ得分<1的碱基

-d 30000表示bam文件的最大测序深度为30000，这是考虑超深度测序的设置

-L 30000表示INDEL序列的最大测序深度为30000，这是考虑超深度测序的设置

```sh
echo varscan
samtools mpileup -f ../../../hg38/hg38.fa Illumina_B1702-sorted.bam > Illumina_B1702.mpileup.txt
varscan mpileup2cns Illumina_B1702.mpileup.txt --output-vcf 1 \ 
--variants 1 --min-var-freq 0.01 > Illumina_B1702.vcf
```

VarScan limit  normal.tumor.vcf.snp  --regions-file  regions.bed  --output-file  normal.tumor.vcf.target.snp

--regions-file指定靶向测序分析的范围

变异过滤：processSomatic命令

VarScan processSomatic  normal.tumor.vcf.target.snp  --min-tumor-freq 0.05 --max-normal-freq 0.15--p-value 0.07

参数说明：这里测序深度较深，所以--max-normal-freq0.15设置较大。

我的个人博客：[http://blog.zd200572.com](http://blog.zd200572.com/)和[www.zd200572.com](http://www.zd200572.com/)