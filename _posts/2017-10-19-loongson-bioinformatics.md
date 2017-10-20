---
layout:     post
title:      龙芯生物信息学软件应用测试
subtitle:   zd00572
date:       2017-10-19
author:     zd200572
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
    - 生物信息
    - bioinformatics
    - 龙芯
    - 测序
---
# 1.平台情况

我是一个龙芯迷，最近在学生物信息，总想尝试一下用龙芯做生物信息的体验，新款的龙芯3A3000买不起。有龙芯吧友贡献了一台龙芯2F在线服务器，可以用来测试软件，刚好我的龙芯小本已挂。所以就用这哥们的机器测试一下，在此对这个哥们表示衷心地感谢！

```sh
#由图中可以看出，这台龙芯笔记本是8.9寸的小本，1g	内存
Linux debian 3.2.0-4-loongson-2f #1 Debian 3.2.51-1 mips64 GNU/Linux
total       used       free     shared    buffers  cached

Mem:          1007        932         75    0        185        613

-/+ buffers/cache:        133        874

Swap:          391          0        391
system type		: lemote-yeeloong-2f-8.9inches
processor		: 0
cpu model		: ICT Loongson-2 V0.3  FPU V0.1
BogoMIPS		: 528.38
wait instruction	: yes
microsecond timers	: yes
tlb_entries		: 64

```

由于十年前的产品，性能就不提了，至少是我们国家的自主产品。

# 2.FASTQC测试

当二代测序的原始数据拿到手之后,第一步要做的就是看一看原始reads的质量。常用的工具就是*fastqc*。

首先，fastqc是基于java的，所以，先安装java，好在龙芯已经移植了，很简单，下载，解压就行。

```sh
#java下载安装
wget http://ftp.loongnix.org/toolchain/java/openjdk6/jdk6-mips32-rc30.tar.gz
tar zxvf jdk6-mips32-rc30.tar.gz
#由于这台机器的环境变量搞不定，就直接路径运行了。
~/test/test-z/j2sdk-image/bin/java -version
java version "1.6.0-internal"
OpenJDK Runtime Environment (build 1.6.0-internal-loongson_14_nov_2016_08_24-b00)
OpenJDK Server VM (build 14.0-b16, mixed mode)
#fastqc下载解压
 wget http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.5.zip #最新版本竟然ok
unzip fastqc_v0.11.5.zip
./fastqc
-bash: ./fastqc: 权限不够
chmod 777 fastqc
 ./fastqc 
Can't exec "java": 没有那个文件或目录 at ./fastqc line 277.
vi fastqc #把java路径改为~/test-z/j2sdk-image/bin/java
./fastqc -v
FastQC v0.11.5 #可以了，搞定
./fastqc ../../test-data/A_1.fastq ../../test-data/A_2.fastq 
Started analysis of A_1.fastq
Approx 50% complete for A_1.fastq
Approx 100% complete for A_1.fastq
Analysis complete for A_1.fastq
Default case invoked for: 
   opcode  = 84, "ConvL2F"
Default case invoked for: 
   opcode  = 84, "ConvL2F"
Started analysis of A_2.fastq
Approx 50% complete for A_2.fastq
Approx 100% complete for A_2.fastq
Analysis complete for A_2.fastq
Default case invoked for: 
   opcode  = 84, "ConvL2F"
Default case invoked for: 
   opcode  = 84, "ConvL2F"
#最后两行不清楚什么情况，有点小问题，不管了，至少还能用。看了一下结果，ok的，正常。

```

![http://owxbk335s.bkt.clouddn.com/loongsonloongson-fastqc.png](http://owxbk335s.bkt.clouddn.com/loongsonloongson-fastqc.png)

开心地看到了正确的质控结果图片！

# 3.picard

也是基于java的，试了一下，没有运行成功，龙芯3a应该是可以的，用jdk8发现运行不起来，这个测试不通过。

```sh
wget https://github.com/broadinstitute/picard/releases/download/2.13.2/picard.jar
#提示java太老了，需要更新，由于只是测试，好像jdk8
Exception in thread "main" java.lang.UnsupportedClassVersionError: picard/cmdline/PicardCommandLine : Unsupported major.minor version 52.0

```



# 4.gatk

也是基于java的，也只支持jdk1.8及以上版本。龙芯3a应该可以。

# 5.bwa-samtools

只提供x86版本二进制文件，所以难以搞定。

# 6.python

```sh
wget https://www.python.org/ftp/python/3.6.3/Python-3.6.3.tgz
tar zxvf Python-3.6.3.tgz
./configure
make #可以正常使用，R,perl也是如此。
```

**综上，用龙芯做生物信息短期内来看还是不现实的，因为生物信息学领域许多软件只提供x86版本二进制文件，java、python、R和perl版的软件还是可以正常运行的。**