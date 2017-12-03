---
layout:     post
title:      HLA-NGS数据处理2
subtitle:   HLA-HD, HLAssign两个软件的使用
date:       2017-12-03
author:     zd200572
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - HLA

---



之前测试了一下使用humanlongevity(文特尔的人类长寿公司)在github上开源的xHLA算法来进行NGS数据的HLA分型，效果还不错，可以实现两位的分型，除了个别等位基因可能不全。

不前天用HLA Typing做关键词搜索了一下论文，发现日本的科学家开发了一款HLA-HD，也是今年发表的，号称可以实现6位分型，好奇心使我测试一下。费了九牛二虎之力，终于运行成功了，无奈手头的测序数据不给力，用弱弱的i3个人电脑挣扎着前后花了两天时间，终于跑出一个只分型两个等位基因的结果，也是醉了。这其中应试有测序深度过低，质量太差的原因，也说明这个软件对测序深度和质量要求较高。

# 1.软件准备

从文章公布的[官网](https://www.genome.med.kyoto-u.ac.jp/HLA-HD/)(https://www.genome.med.kyoto-u.ac.jp/HLA-HD/)申请即可下载，声明是说只能用于学术目的，但看整个过程没有审核机制，也就是注册一个wordpress（官网是用它搭建的）帐号，然后就发邮件告诉你下载地址笔密码了。

下载下来就是解压，然后只要已经装好了bowtie2，gcc，就可以按照官网运行一下`sh install.sh`正常使用了。

# 2.无比艰辛地使用过程

这个软件的软件说明已经写得比较详细了，但是由于可能我是一新手，或者与软件作者的逻辑不一致，走了许多弯路。

## 2.1 软件运行命令

作者要求了必须要把软件目录加入系统环境变量，我自做聪明没有加入（感觉绝对路径运行也不错呀，但是它有多个程序在pipeline里，后面会报错，还是严格遵守作者指南的好），导致软件运行报错，找不到程序，这种低级错误就不表了。



关于这个软件运行说明的命令，我理解了好久才明白，由于电脑性能差，运行一次要八个小时。。。。。。所以破费了不只两天的时间。来，看看这个让人忧伤的命令，哈哈！



```sh
#Running

#Before running the HLA-HD, check the value of open files on your computer by typing:
> ulimit -Sa
#If open files are less than 1024, please type:
> ulimit -n 1024
#or change /etc/security/limits.conf according to your system environment.

#If you have fastq.gz file, unzip gz file in advance. 

#You can run the HLA-HD by typing the following commands:
> hlahd.sh -t [thread_num] -m [minimum length of reads] -c [trimming rate] -f [path_to freq_data directory] fastq_1 fastq_2 gene_split_filt path_to_dictionary_directory IDNAME[any name] output_directory

#For example:
> hlahd.sh -t 2 -m 100 -f freq_data/ data/sample_1.fastq data/sample_2.fastq HLA_gene.split.txt dictionary/ sampleID estimation
```

就是这个dictionary，我没有理清，因为软件帮助里给的是另一个名字， HLA_Div_fasta，最后明白了两个是一个意思，于是搞定，尽管，运行结果。。。

## 2.2 运行过程

我的命令：

```sh

biolinux@E431[hlahd.1.0.0] hlahd.sh -t 4 -f freq_data/ /media/biolinux/LENOVO_imcdul/hla20171102/filter/HLA-1_S82_L001_R1_001.fastq /media/biolinux/LENOVO_imcdul/hla20171102/filter/HLA-1_S82_L001_R2_001.fastq HLA_gene.split.txt dictionary hla-1 /media/biolinux/LENOVO_imcdul/hla-hd-result 
110124 reads; of these:
  110124 (100.00%) were unpaired; of these:
    16243 (14.75%) aligned 0 times
    1095 (0.99%) aligned exactly 1 time
    92786 (84.26%) aligned >1 times
85.25% overall alignment rate
110124 reads; of these:
  110124 (100.00%) were unpaired; of these:
    18178 (16.51%) aligned 0 times
    1763 (1.60%) aligned exactly 1 time
    90183 (81.89%) aligned >1 times
83.49% overall alignment rate
93879 reads; of these:
  93879 (100.00%) were unpaired; of these:
    88312 (94.07%) aligned 0 times
    2703 (2.88%) aligned exactly 1 time
    2864 (3.05%) aligned >1 times
5.93% overall alignment rate
91946 reads; of these:
  91946 (100.00%) were unpaired; of these:
    91788 (99.83%) aligned 0 times
    74 (0.08%) aligned exactly 1 time
    84 (0.09%) aligned >1 times
0.17% overall alignment rate
93879 reads; of these:
  93879 (100.00%) were unpaired; of these:
    92726 (98.77%) aligned 0 times
    1145 (1.22%) aligned exactly 1 time
    8 (0.01%) aligned >1 times
1.23% overall alignment rate
91946 reads; of these:
  91946 (100.00%) were unpaired; of these:
    91177 (99.16%) aligned 0 times
    769 (0.84%) aligned exactly 1 time
    0 (0.00%) aligned >1 times
0.84% overall alignment rate
87270 reads; of these:
  87270 (100.00%) were unpaired; of these:
    2472 (2.83%) aligned 0 times
    60 (0.07%) aligned exactly 1 time
    84738 (97.10%) aligned >1 times
97.17% overall alignment rate
91021 reads; of these:
  91021 (100.00%) were unpaired; of these:
    4228 (4.65%) aligned 0 times
    749 (0.82%) aligned exactly 1 time
    86044 (94.53%) aligned >1 times
95.35% overall alignment rate
87270 reads; of these:
  87270 (100.00%) were unpaired; of these:
    59884 (68.62%) aligned 0 times
    8952 (10.26%) aligned exactly 1 time
    18434 (21.12%) aligned >1 times
31.38% overall alignment rate
91021 reads; of these:
  91021 (100.00%) were unpaired; of these:
    59726 (65.62%) aligned 0 times
    10178 (11.18%) aligned exactly 1 time
    21117 (23.20%) aligned >1 times
34.38% overall alignment rate
17029 reads; of these:
  17029 (100.00%) were unpaired; of these:
    102 (0.60%) aligned 0 times
    0 (0.00%) aligned exactly 1 time
    16927 (99.40%) aligned >1 times
99.40% overall alignment rate
2871 reads; of these:
  2871 (100.00%) were unpaired; of these:
    15 (0.52%) aligned 0 times
    1 (0.03%) aligned exactly 1 time
    2855 (99.44%) aligned >1 times
99.48% overall alignment rate
93879 reads; of these:
  93879 (100.00%) were unpaired; of these:
    63306 (67.43%) aligned 0 times
    11197 (11.93%) aligned exactly 1 time
    19376 (20.64%) aligned >1 times
32.57% overall alignment rate
91946 reads; of these:
  91946 (100.00%) were unpaired; of these:
    59767 (65.00%) aligned 0 times
    10966 (11.93%) aligned exactly 1 time
    21213 (23.07%) aligned >1 times
35.00% overall alignment rate
```

最后的结果：

```sh
A	HLA-A*24:02:01	HLA-A*33:03:01
B	HLA-B*58:01:01	HLA-B*15:01:01
C	HLA-C*03:02:01	HLA-C*04:01:01
DRB1	Not typed	Not typed
DQA1	Not typed	Not typed
DQB1	HLA-DQB1*05:03:01	HLA-DQB1*02:01:01
DPA1	Not typed	Not typed
DPB1	Not typed	Not typed
DMA	Not typed	Not typed
DMB	Not typed	Not typed
DOA	Not typed	Not typed
DOB	Not typed	Not typed
DRA	Not typed	Not typed
DRB3	Not typed	Not typed
DRB4	Not typed	Not typed
E	Not typed	Not typed
F	Not typed	Not typed
G	Not typed	Not typed
H	Not typed	Not typed
J	Not typed	Not typed
K	Not typed	Not typed
L	Not typed	Not typed
```



这就是传说中有6位，好像是平常说的三位吧，只有4个基因成功。论文中最低的测序深度平均是133的，我的数据大概是30X，差得太多了应试是。

# 3.其他的软件

还有一个**HLAssign**，可以可视化比对，然后手动判读，有windows版本，这个门槛低，赞一个，但是需要四核心，8g以上内存，但是现在电脑主流也可以达到了哈。放上官网地址：http://www.ikmb.uni-kiel.de/resources/download-tools/software/hlassign



另一个是**HLAreporter**，这篇日本人文献里说准确率也比较好的，一个香港大学的中国人写的，安装成功了，没有成功运行出结果，才开始是samtools升级后的命令改变，改脚本文件无果后只有去改samtools到0.1.19版本却还是报错，也是醉了，生信软件的兼容性，特别是作者好久不更新之后（2015年发表）。docker运行竟然还出错是，应该是没把所有的运行环境封装进去。



还有是**optiType**，一个德国教授写的软件，只对classI分型，也是docker，却也没有运行成功。。。报错找不到文件，或许读读文章可以找到答案，还可以试试源码安装。

最后是**HLA-PRG-LA**，号称很消耗硬件的，找了一个docker也没有运行成功。。。还有其他的，看文章里都说正确率不好，就没尝试了。