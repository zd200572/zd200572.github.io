---
layout:     post
title:      WES学习笔记
subtitle:   zd00572
date:       2017-10-14
author:     zd200572
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
    - 生物信息
    - bioinformatics
    - notes
    - WES
---
尝试一下jimmy的WES流程，虽然现在云生信势头正猛，做生信的门槛对普通人来说降低了，对专业人士提高了许多，但是谁能阻止我们学习的步伐呢？相信那句「没有白走的路」，继续学习，学习是我的爱好和乐趣。

> 这是生信技能树上帖子的地址，上面有所有代码，赞！一个如此热爱分享的大神！http://www.biotrainee.com/thread-122-1-1.html

# 一、软件和数据准备

## 1.软件安装 

我的原则是能用conda解决的不去wget，所以就conda解决了大部分软件安装问题。我的系统黑苹果10.11.5（EI Capitan），远景论坛上下载的大神配置好的clover配置文件，基本完美，我们的目的不是装系统，而是用嘛，所以也不深入研究了。

```shell
 thinkpad-E431
 处理器：Intel Core i3-3120M	2*2.49 GHz
 内存：12 GB
```

```shell
conda install bwa
#bwa是基于BWT的生物序列比对工具:bwa是为二代测序的短序列比对参考序列（reference，fasta格式）而开发的比对软件。
conda install samtools
#samtools是目前广泛使用额关于处理bam/sam文件的工具。从测序仪得到的fastq文件经过mapping后得到二进制的bam文件，而sam则是它的十进制版本。
conda install gatk
#gatk主要用于从sequencing 数据中进行variant calling，包括SNP、INDEL。比如现在风行的exome sequencing找variant，一般通过BWA+GATK的pipeline进行数据分析。
wget https://software.broadinstitute.org/gatk/download/auth?package=GATK
#上面只是安装了个gatk-register，仍需要下载gatk用gatk-register安装
tar -jxvf GenomeAnalysisTK-3.8-0.tar.bz2
cd GenomeAnalysisTK-3.8-0-ge9d806836/
mv GenomeAnalysisTK.jar ../../biosofts/
gatk-register ~/biosofts/GenomeAnalysisTK.jar
#拷贝到目标文件夹(安装目录)

conda install picard
#picard是一套操作高通量测序（HTS）数据的命令行工具(java)，格式如SAM/BAM/CRAM和VCF。这些文件格式是在Hts规范存储库中定义的。尤其是SAM规范和VCF规范。
```

## 2.数据准备

### 1）模拟产生数据

因为实际的数据太大了，对我这种弱弱的计算机简直是一种折磨，我下过全部的sra序列，转换成fastq后来比对，比对就是花了几小时，什么动静也没有。所以，对于学习来说，产生一点模拟数据是不错的，jimmy人性化的为我们提供了pirs这个软件来模拟产生测序数据。

我表示装这个软件折腾了良久，不过终于可以使用了。首先这个软件依赖于zlib和boost编译，我才开始尝试下载源码编译，好像是成功了。但是，我不放心，于是用brew安装了一下测试了一下。

```sh
brew install zlib
brew install boost
```

然后是pirs这个软件的安装：

大概我只是按步骤装了下就可以用了，中间有点报错，是sh文件里有个路径错误，我还以为是软件的严重错误。

```sh
wget ftp://ftp.genomics.org.cn/pub/pIRS/pIRS_111.tgz #下载软件

tar zxvf pIRS_111.tgz #解压

cd pIRS_111/

make #提示说没有源码不需要编译于是尝试运行了一下，竟然可以运行。
```

```sh
mkdir -p data reference 
pirs simulate -i reference/chr1.fa \
-s ~/biosofts/pirs/pIRS_111/Profiles/Base-Calling_Profiles/humNew.PE100.matrix.gz \
-d ~/biosofts/pirs/pIRS_111/Profiles/GC-depth_Profiles/humNew.gcdep_200.dat  \
-b ~/biosofts/pirs/pIRS_111/Profiles/InDel_Profiles/phixv2.InDel.matrix \
-l 100 -x 50 -Q 33 -o A
```

pirs软件参数学习：

simulate：模拟illumina reads数据

-i：参考基因组序列

-s <double> 杂合 SNP rate (default=0.001)

-d <double> GC内容覆盖深度？

 -b <string> input InDel-error profile,input InDel-error profile for simulating InDel-error of reads, (default=(exe_path)/Profiles/InDel_Profiles/phixv2.InDel.matrix)

-l:read读长

-x:测序覆盖深度，默认5

-Q:33/64

-o <string> output prefix (default=Illumina)

```shell
#程序运行过程：
Start to preview error profile...
In Base-calling profile:
	Ref_Base_num: 4
	Statistical_Cycle_num: 200
	Seq_Base_num: 4
	Quality_num: 41
	100bp reads total average substitution error rate: 0.00372389
Start to construct simulation matrix...
Loading file: /Users/zd200572/biosofts/pirs/pIRS_111/Profiles/Base-Calling_Profiles/humNew.PE100.matrix.gz
Have finished constructing Base-calling simulation matrix1
Start to construct simulation matrix...
Loading file: /Users/zd200572/biosofts/pirs/pIRS_111/Profiles/Base-Calling_Profiles/humNew.PE100.matrix.gz
Have finished constructing Base-calling simulation matrix2
Loading the GC bias profile: /Users/zd200572/biosofts/pirs/pIRS_111/Profiles/GC-depth_Profiles/humNew.gcdep_200.dat

Have finished constructing GC bias simulation matrix
Start to construct InDel-error matrix...
Loading file: /Users/zd200572/biosofts/pirs/pIRS_111/Profiles/InDel_Profiles/phixv2.InDel.matrix

For simulating GC bias:
	GC%	abundance
	0	0.00422544
	1	0.00624158
	2	0.00912628
	...
In InDel-error profile:
	profile_Cycle_num: 200
	read1 count: 147091454
	read2 count: 145785569
	length of max InDel: 3
	insertion-base rate of 100-bp read1: 4.77512e-06
	deletion-base rate of 100-bp read1: 1.11823e-05
	insertion-base rate of 100-bp read2: 8.36749e-06
	deletion-base rate of 100-bp read2: 1.55069e-05
Have finished constructing InDel-error simulation matrix
Have finished reading scaffold chr1
Begin to output reads...
Output 10000 pair reads
Output 20000 pair reads
...
Finish output reads

#由于50x速度实在生成的太慢，2x的试试，哈哈475s搞定。

In ouput data:
	sum of Insertion in read1 file: 1211
	sum of Deletion in read1 file: 2814
	sum of Insertion in read2 file: 2103
	sum of Deletion in read2 file: 3825
All done! Run time: 475s.
#对比一下50x的
In ouput data:
	sum of Insertion in read1 file: 30374
	sum of Deletion in read1 file: 70211
	sum of Insertion in read2 file: 52633
	sum of Deletion in read2 file: 95478
All done! Run time: 11248s.
```

### 2）真实的wes数据（不是必需）

没看到在流程中用到，下下来以后备用，有100G之巨。测试了一下，对于我的电脑配置，单单bwa比对运行要花100个小时。。。

```sh
# ~100GB disk space required to download the NA12878

wget [url]ftp://ftp.sra.ebi.ac.uk/vol1/fastq/ERR262/ERR262997/ERR262997_1.fastq.gz[/url]
wget [url]ftp://ftp.sra.ebi.ac.uk/vol1/fastq/ERR262/ERR262997/ERR262997_2.fastq.gz[/url]
```

### 3）参考基因组

```sh
cd reference
wget http://hgdownload.cse.ucsc.edu/goldenPath/hg38/bigZips/hg38.chromFa.tar.gz
tar zxvf hg38.chromFa.tar.gz
cd chroms
for i in $(seq 1 22) X Y M; do cat chr${i}.fa >> hg19.fasta; done
cp chr1.fa ../
rm -fr chr*.fasta
cd ../
```

### 4）基因组index和dictionary的获得

```sh
bwa index -p hg38.chr1 chr1.fa
samtools faidx hg38.fa
picard CreateSequenceDictionary.jar R=hg38.fasta O=hg38.dict
```

### 5）其他参考数据

```sh
# dbSNP138
 wget http://hgdownload.cse.ucsc.edu/goldenPath/hg38/database/snp150.txt.gz

# GATK resource bundle

GATK_FTP=ftp://gsapubftp-anonymous@ftp.broadinstitute.org/bundle/2.8/hg38

# download library file for GATK's VariantRecalibrator

for f in hapmap_3.3.hg38.vcf.gz 1000G_omni2.5.hg38.vcf.gz 1000G_phase1.indels.hg38.vcf.gz Mills_and_1000G_gold_standard.indels.hg38.vcf.gz
do
curl --remote-name ${GATK_FTP}/${f}
done
```

# 二、软件运行

## 1.bwa比对

由于对于一个软件来说，功能太多，不可能一一覆盖，于是，我就先学习这次用到的参数，顺便对软件做一个大概了解，由于是初学，目标先定低一点，先了解大概，以后做项目再一一学习。

bwa的mem参数：MEM是bwa中最新的算法，基本取代了前两种，目的是将测序reads或组装的contig比对到Reference上。（Bio-Xin博客：http://www.cnblogs.com/leezx/p/6226717.html）

-t参数，线程数；-R参数：设置reads标头，“\t”分割；M——将较短的split hits标记为secondary，与picard兼容；后边跟参考基因组、reads文件和>以及要生成的sam文件。（如果GATK call SNP 必须用-r 参数）

```sh
R1=/mnt/A_100_500_1.fq.gz
R2=/mnt/A_100_500_2.fq.gz
#align with BWA, with 4 threads (-t 4). Reading Group is required (-R ...).
bwa mem -t 4 -R '@RG\tID:group_id\tPL:illumina\tSM:sample_id' $DATA/hg19.chr1/hg19.chr1 ${R1} ${R2} > A.chr1.sam
Real time: 457.713 sec; CPU: 1489.602 sec
#2x的数据
 Real time: 12440.568 sec; CPU: 43493.514 sec #50x
```

## 2.picard

### 1）SortSam工具

由BWA生成的sam文件时按字典式排序法进行的排序（lexicographically）进行排序的（chr10，chr11…chr19，chr1，chr20…chr22，chr2，chr3…chrM，chrX，chrY），但是GATK在进行callsnp的时候是按照染色体组型（karyotypic）进行的（chrM，chr1，chr2…chr22，chrX，chrY），因此要对原始sam文件进行reorder。可以使用picard-tools中的ReorderSam完成，同时格式转换成了bam。（https://www.plob.org/article/7009.html）

```sh
picard SortSam CREATE_INDEX=True SORT_ORDER=coordinate VALIDATION_STRINGENCY=LENIENT INPUT=A.chr1.sam OUTPUT=A.chr1.sort.bam
#2x运行情况 
picard.sam.SortSam done. Elapsed time: 4.54 minutes.
Runtime.totalMemory()=872415232
#50x
```

 ### 2）MarkDuplicates工具

过量扩增的reads并不是基因组自身固有序列，不能作为变异检测的证据，因此，要尽量去除这些由PCR扩增所形成的duplicates，这一步可以使用picard-tools来完成。去重复的过程是给这些序列设置一个flag以标志它们，方便GATK的识别。还可以设置 REMOVE_DUPLICATES=true 来丢弃duplicated序列。对于是否选择标记或者删除，对结果应该没有什么影响，GATK官方流程里面给出的例子是仅做标记不删除。这里定义的重复序列是这样的：如果两条reads具有相同的长度而且比对到了基因组的同一位置，那么就认为这样的reads是由PCR扩增而来，就会被GATK标记。

```sh
picard MarkDuplicates CREATE_INDEX=true REMOVE_DUPLICATES=True ASSUME_SORTED=True VALIDATION_STRINGENCY=LENIENT METRICS_FILE=/dev/null INPUT=A.chr1.sort.bam OUTPUT=A.chr1.sort.dedup.bam
#2x运行情况
picard.sam.markduplicates.MarkDuplicates done. Elapsed time: 5.15 minutes.
Runtime.totalMemory()=822083584
```

### 3）FixMateInformation

这一步骤在网上搜到了这个。。。（看来我得好好理出一个现在使用的流程来，生物信息的流程发展还真是快呀！）在一些老版本的pipeline中(如seqanswers上的那个)，这一步做完后还要对pair-end数据的mate information进行fix。不过新版本已经不需要这一步了，Indel realign可以自己fix mate。（http://www.bbioo.com/lifesciences/40-115982-1.html）

```sh
picard FixMateInformation SO=coordinate VALIDATION_STRINGENCY=LENIENT CREATE_INDEX=true INPUT=A.chr1.sort.dedup.bam OUTPUT=A.chr1.sort.dedup.mate.bam
#2x运行情况
picard.sam.FixMateInformation done. Elapsed time: 6.36 minutes.
Runtime.totalMemory()=877658112
```

## 3.gatk

终于到了大头gatk出场了，我表示我对它好陌生，几乎是第一次运行它。通过上面可以看出他是一个经常更新的程序，而且它虽然是一个java程序，但是它有好几个子工具，就像上面的picard。先看看它的流程，官方的：

![https://software.broadinstitute.org/gatk/img/BP_workflow_3.6.png](https://software.broadinstitute.org/gatk/img/BP_workflow_3.6.png)

### 1)RealignerTargetCreator

对INDEL周围进行realignment，这个操作有两个步骤，第一步生成需要进行realignment的位置的信息, 输出一个包含着possible indels的文件。

```sh
GenomeAnalysisTK -R reference/chr1.fa \
-T RealignerTargetCreator \
-I A.chr1.sort.dedup.mate.bam -o A.intervals
```

### 2)IndelRealigner

第二步才是对这些位置进行realignment, 最后生成一个realin好的BAM文件sample.realn.bam

```sh
GenomeAnalysisTK -R reference/chr1.fa \
-T IndelRealigner \
-targetIntervals A.intervals \
-I A.chr1.sort.dedup.mate.bam -o A.chr1.sort.dedup.mate.relaign.bam
```

### 3)BaseRecalibrator

（对base的quality score进行校正）碱基质量分数重校准（Base quality score recalibration，BQSR)，就是利用机器学习的方式调整原始碱基的质量分数。它分为两个步骤:

1. 利用已有的snp数据库，建立相关性模型，产生重校准表( recalibration table)

2. 根据这个模型对原始碱基进行调整，只会调整非已知SNP区域。

   （参考自生信媛--GATK之BaseRecalibrator）

```sh
GenomeAnalysisTK -R reference/chr1.fa \
-T BaseRecalibrator \
-knownSites $DATA/dbsnp_138.hg19.vcf \
-o A.recal \
-I A.chr1.sort.dedup.mate.relaign.bam
```

### 4）UnifiedGenotyper

这一步提示jimmy的代码不能用了，说3.7以后采用了新的参数，更新好快。

使用`UnifiedGenotyper`寻找variant。论坛搜索发现，现在推荐用`HaplotypeCaller`，效果更好。

```sh
GenomeAnalysisTK -T UnifiedGenotyper -R chr1.fa -I A.chr1.sort.dedup.mate.relaign.recal.bam --dbsnp ../common_all_20170710.vcf -o snps.raw.vcf -stand_call_conf 50.0
```

### 5）HaplotypeCaller

同样是更新了的参数处理方式。

> 由于**HaplotypeCaller**的工作原理，直接省去了BQSR和indel realignment步骤，所以对于一个variant calling流程而言，可以直接比对，去重复后运行**HaplotypeCaller**。
>
> HaplotypeCaller，简称HC，能过通过对活跃区域（也就是与参考基因组不同处较多的区域）局部重组装，同时寻找SNP和INDEL。换句话说，当HC看到一个地方好活跃呀，他就不管之前的比对结果了，直接对这个地方进行重新组装，所以就比传统的基于位置（position-based)的工具，如前任UnifiedGenotyper好用多了。
>
> HC可以处理非二倍体物种和混池实验数据，但是不推荐用于癌症或者体细胞。
> HC还可以正确处理可变剪切，所以也能用于RNA-Seq数据。
>
> 参考自生信媛--生信媛的GATK大礼包 

> ```sh
> GenomeAnalysisTK -R chr1.fa -T HaplotypeCaller --dbsnp ../common_all_20170710.vcf -stand_call_conf 30 -o A.hc.vcf -I A.chr1.sort.dedup.mate.relaign.recal.bam
> ```

# 4.总结

虽然马马虎虎走了一次最基本的几个步骤，发现学习之路任重而道远呀！我只是个初学者，加油！



