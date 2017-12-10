---
layout:     post
title:      CHIP-seq实际操作（续） 
subtitle:   学习自生技能树论坛
date:       2017-11-19
author:     zd200572
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - Bioinformatics
    - Notes
    - 生物信息
    - CHIP-seq
---

# CHIP-seq实际操作（续3-） #
首先声明，虽然是实战，但是其实是学习笔记而已，初学，参考了大量大神的博客和帖子,还有大神引用的大牛的帖子,参考列表见最后。隔了好久了，来更新一下，证明我没有停下来，只是有点慢。。。3-fastq和4-参考基因组已经在转录组的时候学习过了，见我的转录组笔记，还是有点遗忘，因为工作中用的不多，加油，复习。



回顾一下前面的步骤，软件准备、数据下载。

# 1.Step5比对

 比对上，没有去读文章，所以脚本解决了，具体的文件编号不够明了，就参考大家的了。

```sh
ls 0_data/*fastq.gz | while read id; do bowtie2 -p 2 -3 5 --local -x reference/mm10 -U $id | samtools sort -O bam -o $id.bam;done
```

bowtie2的几个参数：

-p是线程，由于同时在做找变异的工作，用了一个线程，为了保险起见，用了两个线程。

3端质量有点问题，用了**-3 5 --local参数**，应试是用于过滤。

```sh
-x <bt2-idx> 由bowtie2-build所生成的索引文件的前缀。首先 在当前目录搜寻，然后
在环境变量 BOWTIE2_INDEXES 中制定的文件夹中搜寻。
-1 <m1> 双末端测寻对应的文件1。可以为多个文件，并用逗号分开；多个文件必须和 -2 
<m2> 中制定的文件一一对应。比如:"-1 flyA_1.fq,flyB_1.fq -2 flyA_2.fq,flyB
_2.fq". 测序文件中的reads的长度可以不一样。
-2 <m2> 双末端测寻对应的文件2.
-U <r> 非双末端测寻对应的文件。可以为多个文件，并用逗号分开。测序文件中的reads的
长度可以不一样。
-S <hit> 所生成的SAM格式的文件前缀。默认是输入到标准输出。
```

# 2.Step6：Call Peaks

```sh
ls 0_data/*fastq.gz | while read id; do bowtie2 -p 4 -3 5 --local -x reference/mm10 -U $id | samtools sort -O bam -o $id.bam;done
ls 0_data/*bam| while read id; do samtools sort $id -o $id.sort.bam;done
ls 0_data/*sort.bam| while read id; do samtools index $id;done
macs2 callpeak -c 0_data/SRR620208.fastq.gz.bam -t 0_data/SRR620206.fastq.gz.bam -q 0.05 -f BAM -g mm -n suz12 2> suz12.macs2.log &
macs2 callpeak -c 0_data/SRR620208.fastq.gz.bam -t 0_data/SRR620204.fastq.gz.bam -q 0.05 -f BAM -g mm -n ring1B 2> ring1B.macs2.log &
macs2 callpeak -c 0_data/SRR620209.fastq.gz.bam -t 0_data/SRR620205.fastq.gz.bam -q 0.05 -f BAM -g mm -n cbx7 2> cbx7.macs2.log &
macs2 callpeak -c 0_data/SRR620209.fastq.gz.bam -t 0_data/SRR620207.fastq.gz.bam -q 0.01 -f BAM -g mm -n RYBP 2>RYBP.macs2.log &
```

## 2.1 macs2参数学习

- -t: 实验组的输出结果

- -c: 对照组的输出结果

- -f: -t和-c提供文件的格式，可以是”ELAND”, “BED”, “ELANDMULTI”, “ELANDEXPORT”, “ELANDMULTIPET” (for pair-end tags), “SAM”, “BAM”, “BOWTIE”, “BAMPE”  “BEDPE” 任意一个。如果不提供这项，就是自动检测选择。

- -g: 基因组大小， 默认提供了hs, mm, ce, dm选项， 不在其中的话，比如说拟南芥，就需要自己提供了。

- -n: 输出文件的前缀名

- -B: 会保存更多的信息在bedGraph文件中，如fragment pileup, control lambda, -log10pvalue and -log10qvalue scores

- -q: q值，也就是最小的PDR阈值， 默认是0.05。q值是根据p值利用BH计算，也就是多重试验矫正后的结果。

- -p： 这个是p值，指定p值后MACS2就不会用q值了。

- -m: 和MFOLD有关，而MFOLD和MACS预构建模型有关，默认是5：50，MACS会先寻找100多个peak区构建模型，一般不用改，因为你不懂。

  ## 2.2 peaks结果

  ```sh
  #ls *.bed | while read id;do {print $id ;  wc -l $id;}done
  wc -l *.bed 这个命令就解决了，上边那条也是多余了。
  11637 cbx7_summits.bed
  8296 ring1B_summits.bed
  6872 RYBP2_s.bed #这个是下载来的
  6872 RYBP2_summits.bed
  146 RYBP_summits.bed
  7636 suz12_summits.bed
  ```

不知道为什么，我的结果比他们的多了好大一部分，同样的代码，也是醉了，难道是软件升级的原因？

**其他结果文件**

- NAME_peaks.xls: 以表格形式存放peak信息，虽然后缀是xls，但其实能用文本编辑器打开，和bed格式类似，但是**以1为基**，而bed文件是**以0为基**.也就是说xls的坐标都要减一才是bed文件的坐标

- NAME_peaks.narrowPeak NAME_peaks.broadPeak 类似。后面4列表示为， integer score for display， fold-change，-log10pvalue，-log10qvalue，relative summit position to peak start。内容和NAME_peaks.xls基本一致，适合用于导入R进行分析。

- NAME_summits.bed：记录每个peak的peak summits，话句话说就是记录极值点的位置。MACS建议用该文件寻找结合位点的motif。

- NAME_model.r，能通过`$ Rscript NAME_model.r`作图，得到是基于你提供数据的peak模型。

  # 3.结果注释和可视化

  ## 3.1 知识学习

  ChIPseeker的功能分为三类:

  - 注释：提取peak附近最近的基因， 注释peak所在区域
  - 比较：估计ChIP peak数据集中重叠部分的显著性；整合GEO数据集，以便于将当前结果和已知结果比较
  - 可视化： peak的覆盖情况；TSS区域结合的peak的平均表达谱和热图；基因组注释；TSS距离；peak和基因的重叠

  完全符合我们的需要，都不需要用到`bedtools`和`deeptools`。ps.我试用jimmy的代码跑bedtools和deeptools失败了，会在第二步报错。代码见下：

  ```sh
  ls 0_data/*sort.bam |while read id
  do
  file=$(basename $id )
  sample=${file%%.*}
  echo $sample
  #bamCoverage -b $id -o $sample.bw -p 4 --normalizeUsingRPKM ## 这里有个参数，
  #break
  computeMatrix reference-point --referencePoint TSS -b 10000 -a 10000 -R 
  #index out of range报错
  reference/mm10_refSeq.bed -S $sample.bw --skipZeros -o matrix1_${sample}_TSS.gz --outFileSortedRegions regions1_${sample}_genes.bed
  plotHeatmap -m matrix1_${sample}_TSS.gz -out ${sample}.png
  break
  done
  ```

  ## 3.2 R代码

  ```R
  #软件安装代码，不用多说
  source("https://bioconductor.org/biocLite.R") 
  options(BioC_mirror="http://mirrors.ustc.edu.cn/bioc/") 
  biocLite("ChIPseeker")
  biocLite("org.Mm.eg.db")
  biocLite("TxDb.Mmusculus.UCSC.mm10.knownGene")
  biocLite("clusterProfiler")
  biocLite("ReactomePA")
  biocLite("DOSE")
  biocLite("clusterProfiler")
  biocLite("org.Mm.eg.db")
  biocLite("TxDb.Mmusculus.UCSC.mm10.knownGene")

  library("ChIPseeker")
  library("org.Mm.eg.db")
  library("TxDb.Mmusculus.UCSC.mm10.knownGene")

  txdb <- TxDb.Mmusculus.UCSC.mm10.knownGene

  library("clusterProfiler")

  #读入bed文件
  setwd("/media/biolinux/LENOVO_imcdul/CHIP-seq")
  ring1B <- readPeakFile("ring1B_peaks.narrowPeak")
  suz12 <- readPeakFile("suz12_peaks.narrowPeak")
  cbx7 <- readPeakFile("cbx7_peaks.narrowPeak")
  RYBP <- readPeakFile("RYBP_peaks.narrowPeak")
  #Chip peaks coverage plot

  #查看peak在全基因组的位置

  covplot(ring1B,chrs=c("chr17", "chr18"))

  #Heatmap of ChIP binding to TSS regions

  promoter <- getPromoters(TxDb=txdb, upstream=3000, downstream=3000)

  tagMatrix <- getTagMatrix(ring1B, windows=promoter)

  tagHeatmap(tagMatrix, xlim=c(-3000, 3000), color="red")

  #Average Profile of ChIP peaks binding to TSS region

  #Confidence interval estimated by bootstrap method

  plotAvgProf(tagMatrix, xlim=c(-3000, 3000), conf = 0.95, resample = 1000)
  #peak的注释
  #ChIPseeker负责注释的就是annotatePeak
  peakAnno <- annotatePeak(ring1B, tssRegion=c(-3000, 3000),
                           
                           TxDb=txdb, annoDb="org.Mm.eg.db")
  #可视化 Pie and Bar plot

  plotAnnoBar(peakAnno)

  vennpie(peakAnno)

  upsetplot(peakAnno)#UpSet的点图，适用于多于5个集合表示情况

  #可视化TSS区域的TF binding loci，看不同蛋白的靶位点的注释情况

  plotDistToTSS(peakAnno,
                
                title="Distribution of transcription factor-binding loci\nrelative to TSS")
  #多个peak的比较，准备TSS区域，然后将peak映射到这些区域，得到tagMatrix

  #多个peak set注释时，先构建list,然后用lapply.list(name1=bed_file1,name2=bed_file2) RYBP的数据有问题，这里加上去，会一直报错。

  peaks <- list(cbx7=cbx7,ring1B=ring1B,suz12=suz12)#

  promoter <- getPromoters(TxDb=txdb, upstream=3000, downstream=3000)

  tagMatrixList <- lapply(peaks, getTagMatrix, windows=promoter)

  plotAvgProf(tagMatrixList, xlim=c(-3000, 3000))

  #plotAvgProf(tagMatrixList, xlim=c(-3000, 3000), conf=0.95,resample=500, facet="row")
  #我遇见的报错信息
  #Error in boot(data = tagMatrix, statistic = getSgn, R = RESAMPLE_TIME,  : 
  #number of items to replace is not a multiple of replacement length
  #tagHeatmap(tagMatrixList, xlim=c(-3000, 3000), color=NULL)
  #参数改成2500就跑出结果了。
  #ChIP peak annotation comparision

  peakAnnoList <- lapply(peaks, annotatePeak, TxDb=txdb,
                         
                         tssRegion=c(-3000, 3000), verbose=FALSE)

  plotAnnoBar(peakAnnoList)

  plotDistToTSS(peakAnnoList)
  #Overlap of peaks and annotated genes

  genes= lapply(peakAnnoList, function(i) as.data.frame(i)$geneId)

  vennplot(genes)
  ```

  得到最基本的peak数据后，我们要做以下事情

  - 大量的韦恩图，描述不同蛋白结合基因的关系
  - 不同蛋白在染色体结合位点与TSS的距离

  为了完成上面说的两件事情，我们需要注释peak，准备TSS所在位置然后把peak比对到这些区域.
  **注：** 原文提供不同蛋白的交集的基因TSS区域，所以要先做注释。

  关于peak注释一定要多说几句：

  - 启动子区域目前没有明确定义，一般认为基因起始转录位点的上下游区域是启动子区域，文章认为是TSS2.5 kb 以内都是靶基因
  - 注释有两类，genomic annotation和nearest gene annotation. 前者是研究直接调控对象，后者是做基因表达调控
  - 还有一类注释就是简单看peak上下游的范围的基因

  根据文章得知需要距离TSS一定距离的注释，以及peak上下5 Kb 的注释。

  **Upset多点图**

  感觉这个图不够直观呢。

  ![](http://owxbk335s.bkt.clouddn.com/upsetplot.png)

  **TSS分布图**

  ![](http://owxbk335s.bkt.clouddn.com/Rplot_TSS.png)

  **reads_frequency**

  ![](http://owxbk335s.bkt.clouddn.com/3gene_reads_count_freq.png)

  **热图**

  ![](http://owxbk335s.bkt.clouddn.com/3genes_heatmap.png)

  **丑怪的venn图**

  ![](http://owxbk335s.bkt.clouddn.com/Rplot.png)

  **我只是模仿了一下大家的实战，R代码学的半调子水平，好好学习，加油呀！**

**参考内容列表：**


>1、[ChIP-seq实战分析](https://mp.weixin.qq.com/s?__biz=MzAxMDkxODM1Ng==&mid=2247484549&idx=1&sn=0221ad954d79634f5fad2ccb565c8652&scene=21#wechat_redirect)
>
>2、[一篇文章学会ChIP-seq分析（上）](https://mp.weixin.qq.com/s?__biz=MzAxMDkxODM1Ng==&mid=2247484370&idx=1&sn=3e29df3b621076bd1d33a8ec157858e5&scene=21#wechat_redirect)
>
>3、[一篇文章学会ChIP-seq分析（下）](https://mp.weixin.qq.com/s?__biz=MzAxMDkxODM1Ng==&mid=2247484372&idx=1&sn=30ad9c4c54f3967000af059eb7a38ace&scene=21#wechat_redirect)
>
>4、了解基础知识
>
>peak calling的统计学原理 http://www.plob.org/2014/05/08/7227.html
>
>根据比对的bam文件来对peaks区域可视化 http://www.bio-info-trainee.com/1843.html
>
>wig、bigWig和bedgraph文件详解 http://www.bio-info-trainee.com/1815.html
>
>5、文章综述
>
>ChIP-seq guidelines and practices of the ENCODE and modENCODE consortia. https://www.ncbi.nlm.nih.gov/pubmed/22955991
