---
layout:     post
title:      质控学习笔记
subtitle:   认识到实践的重要性
date:       2017-11-13
author:     zd200572
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - 生物信息
    - Notes
    - QC
---

# 质控学习笔记

##1.初识质控的重要性

搞了一堆测序数据，往程序一丢，以为就是生信的分析过程，真正的是要理解每个工具有作用，去根据真正的情况实现正确的处理。拿到一堆数据忙乱如麻大概就是我等小白的水平了，还好有大神的文章引路。

>这里放上我参考的文章：
>
>[要充分了解你的测序数据--论QC的重要性](http://www.biotrainee.com/thread-324-1-1.html)
>
>### NGS测序数据的*质量*控制 (*Quality* Control,QC)--[生信媛](http://mp.weixin.qq.com/profile?src=3&timestamp=1510558460&ver=1&signature=TtT-Ig9-yaFMI*nR8sHXUak*pl3UBhJlGZNQbJc*ybFx1hRx9wSMvzKS4rkKVYbfYL4TCvAVbS*uNNukOSHDVw==)

### 2.我的质控探索

1）先看看这惨不忍睹的测序数据：

![](http://owxbk335s.bkt.clouddn.com/qc-raw.png)

190以后就低于q20了，2*300PE。

2）Q20过滤一下

```sh
trimmomatic SE ../HLA-1_S82_L001_R1_001.fastq HLA-1-1.fastq AVGQUAL:20
#Input Reads: 110124 Surviving: 109315 (99.27%) Dropped: 809 (0.73%)
```

![](http://owxbk335s.bkt.clouddn.com/qc-1-1.png)

过滤掉了0.73%，看看情况，好像没什么效果：

继续，加上长度过滤呢：

```sh
trimmomatic SE ../HLA-1_S82_L001_R1_001.fastq HLA-1-2.fastq TRAILING:20 MINLEN:150
#Input Reads: 110124 Surviving: 110100 (99.98%) Dropped: 24 (0.02%)
```

![](http://owxbk335s.bkt.clouddn.com/qc-1-2.png)



依然没有什么效果呢。

3）滑窗的方法过滤：

```sh
trimmomatic SE ../HLA-1_S82_L001_R1_001.fastq HLA-1-3.fastq SLIDINGWINDOW:3:20 MINLEN:150
#Input Reads: 110124 Surviving: 93050 (84.50%) Dropped: 17074 (15.50%)
```

![](http://owxbk335s.bkt.clouddn.com/qc-1-3.png)

终于全部q20以上了，目标初步完成，测试一下，运行程序，结果还可以，就这样了。把丢弃reads长度的阀值往下放点可以获得更多的数据，由于我此次过滤另一个目的在于减少程序的内存占用，于是就用了150。

具体的差别对这次的数据来说是这样的：

```sh
biolinux@E431[trim]  trimmomatic SE ../HLA-1_S82_L001_R1_001.fastq HLA-1-5.fastq SLIDINGWINDOW:3:20 MINLEN:280
#TrimmomaticSE: Started with arguments:
# ../HLA-1_S82_L001_R1_001.fastq HLA-1-5.fastq SLIDINGWINDOW:3:20 MINLEN:280
#Automatically using 4 threads
#Quality encoding detected as phred33
#Input Reads: 110124 Surviving: 1533 (1.39%) Dropped: 108591 (98.61%)
#TrimmomaticSE: Completed successfully
biolinux@E431[trim]  trimmomatic SE ../HLA-1_S82_L001_R1_001.fastq HLA-1-5.fastq SLIDINGWINDOW:3:20 MINLEN:260
#TrimmomaticSE: Started with arguments:
# ../HLA-1_S82_L001_R1_001.fastq HLA-1-5.fastq SLIDINGWINDOW:3:20 MINLEN:260
#Automatically using 4 threads
#Quality encoding detected as phred33
#Input Reads: 110124 Surviving: 5924 (5.38%) Dropped: 104200 (94.62%)
#TrimmomaticSE: Completed successfully
biolinux@E431[trim]  trimmomatic SE ../HLA-1_S82_L001_R1_001.fastq HLA-1-5.fastq SLIDINGWINDOW:3:20 MINLEN:220
#TrimmomaticSE: Started with arguments:
# ../HLA-1_S82_L001_R1_001.fastq HLA-1-5.fastq SLIDINGWINDOW:3:20 MINLEN:220
#Automatically using 4 threads
#Quality encoding detected as phred33
#Input Reads: 110124 Surviving: 41060 (37.29%) Dropped: 69064 (62.71%)
#TrimmomaticSE: Completed successfully
```

