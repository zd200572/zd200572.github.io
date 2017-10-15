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



```
mkdir -p data reference 
pirs simulate -i reference/chr1.fa \
-s ~/biosofts/pirs/pIRS_111/Profiles/Base-Calling_Profiles/humNew.PE100.matrix.gz \
-d ~/biosofts/pirs/pIRS_111/Profiles/GC-depth_Profiles/humNew.gcdep_200.dat  \
-b ~/biosofts/pirs/pIRS_111/Profiles/InDel_Profiles/phixv2.InDel.matrix \
-l 100 -x 50 -Q 33 -o A
```

pirs软件参数学习：



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

没看到在流程中用到，下下来以后备用，有100G之巨。

```sh
# ~100GB disk space required to download the NA12878

wget [url]ftp://ftp.sra.ebi.ac.uk/vol1/fastq/ERR262/ERR262997/ERR262997_1.fastq.gz[/url]
wget [url]ftp://ftp.sra.ebi.ac.uk/vol1/fastq/ERR262/ERR262997/ERR262997_2.fastq.gz[/url]
```

### 3）参考基因组

```
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

```
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

```sh
R1=/mnt/A_100_500_1.fq.gz
R2=/mnt/A_100_500_2.fq.gz
#align with BWA, with 4 threads (-t 4). Reading Group is required (-R ...).
bwa mem -t 4 -R '@RG\tID:group_id\tPL:illumina\tSM:sample_id' $DATA/hg19.chr1/hg19.chr1 ${R1} ${R2} > A.chr1.sam
Real time: 457.713 sec; CPU: 1489.602 sec
#2x的数据
 Real time: 12440.568 sec; CPU: 43493.514 sec #50x
```

```sh
picard SortSam CREATE_INDEX=True SORT_ORDER=coordinate VALIDATION_STRINGENCY=LENIENT INPUT=A.chr1.sam OUTPUT=A.chr1.sort.bam
#2x运行情况 
picard.sam.SortSam done. Elapsed time: 4.54 minutes.
Runtime.totalMemory()=872415232
#50x

```

 

```sh
picard MarkDuplicates CREATE_INDEX=true REMOVE_DUPLICATES=True ASSUME_SORTED=True VALIDATION_STRINGENCY=LENIENT METRICS_FILE=/dev/null INPUT=A.chr1.sort.bam OUTPUT=A.chr1.sort.dedup.bam
#2x运行情况
picard.sam.markduplicates.MarkDuplicates done. Elapsed time: 5.15 minutes.
Runtime.totalMemory()=822083584
```



```sh
picard FixMateInformation SO=coordinate VALIDATION_STRINGENCY=LENIENT CREATE_INDEX=true INPUT=A.chr1.sort.dedup.bam OUTPUT=A.chr1.sort.dedup.mate.bam
#2x运行情况
picard.sam.FixMateInformation done. Elapsed time: 6.36 minutes.
Runtime.totalMemory()=877658112
```



