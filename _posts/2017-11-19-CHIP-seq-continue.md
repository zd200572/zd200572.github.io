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

# 1.Step5比对

 比对上，没有去读文章，所以脚本解决了，具体的文件编号不够明了，就参考大家的了。

```sh
ls 0_data/*fastq.gz | while read id; do bowtie2 -p 2 -3 5 --local -x reference/mm10 -U $id | samtools sort -O bam -o $id.bam;done
```

bowtie2的几个参数：

-p是线程，由于同时在做找变异的工作，用了一个线程，为了保险起见，用了两个线程。

3端质量有点问题，用了**-3 5 --local参数**，应试是用于过滤。

```
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

参考内容列表：


>1、
>
>2、
>
>3、
>
>4、
>
>5、 
>
>6、
>
