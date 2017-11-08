---
layout:     post
title:      GATK软件配套资源中心有什么，如何获取？
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
[GATK中文社区](https://www.gatk.com.cn)

[gatk-chinese github](https://github.com/gatk-chinese)

[生信技能树](http://www.biotrainee.com)

**有幸参加gatk中文文档的翻译工作，感觉还是好自豪的，虽然我还不是生信从业者，可以以这样的方式为这个行业做点事情，这就是动力！感谢jimmy和生信技能树！这是第一篇：**

原文链接  ： [[ What's in the resource bundle and how can I get it?](https://software.broadinstitute.org/gatk/documentation/article?id=1213)](https://software.broadinstitute.org/gatk/documentation/article?id=1213)

注意：我们最近对FTP服务器上的包进行了一些更改，详情请参见参考资料包页。 简而言之：小目录结构的变化，并将Hg38包镜像了云版本。

------

### 1. 获取包

参见 [资源包](https://software.broadinstitute.org/gatk/download/bundle)页。简而言之，有谷歌云版本和一个FTP服务器。谷歌云版本只有hg38的资源；其他版本的资源目前仅可通过FTP服务器使用。 如果你也希望它们在云上，请告知我们。

------

### 2. Grch38 / Hg38资源：即将成为标准数据集

这包含全基因组测序数据（WGS）分析最佳实践中短突变发现所需的所有资源文件。 外显子组文件和逐项资源列表即将推出（ish）。

------

#### 以下所有资源仅在FTP服务器上可用，在云上不可用。

------

### 3. b37资源:hg38包完成之前的标准数据集

- 参考序列(标准的千人基因组fasta)以及fai和dict文件

- vcf格式的dbsnp。这包括两个文件:

  - 最近的dbsnp版本(build 138)
  - 此文件仅指向在dbsnp build 129中或之前发现的位点，它排除了千人基因组项目的影响，并有助于评估dbsnp新位点的比例和ti /TV值。

- hapmap基因型和位点的VCFs

- 千人基因组计划OMNI数据库2.5的基因型和位点, VCF

- 用于本地重新比对的已知当前最好的indel数据集（请注意，我们不再使用dbSNP了）； 使用这两个文件：

  - 1000G_phase1.indels.b37.vcf (目前来自千人基因组计划第一阶段indel calls)
  - Mills_and_1000G_gold_standard.indels.b37.sites.vcf

- 最新的千人基因组计划第三阶段 (v4)数据集，用于基因型的优化: 1000G_phase3_v4_20130502.sites.vcf

- 用于测试的大规模标准单样本bam文件: 

  - NA12878.HiSeq.WGS.bwa.cleaned.recal.b37.20.bam包含染色体20上NA12878测序深度为~64x的reads 
  - 通过在上面的数据集上运行unifiedgenotyper生成的调用。请注意，此资源已过时，不代表我们最佳实践的结果。这将在不久的将来更新。

- Broad定制的外显子组的靶向区域列表：

  Broad.human.exome.b37.interval_list (请注意，您应该始终使用适合您数据的外显子组靶向区域列表，这通常取决于制备试剂盒，并且应该在制造商的网站上提供。)

此外，这些文件都有补充索引，统计信息和其他QC数据。

------

### 4. hg19资源：从b37转换

包括ucsc风格的hg19参考资料，以及所有转换的VCF文件。

------

### 5. hg18资源：从b37转换

包括ucsc风格的hg18参考资料，以及所有的VCF文件。refGene track和BAM文件不可用。我们只为这个基因组构建提供数据文件，它可以从我们的master b37库中“轻松”地转换。对于这可能造成的不便表示抱歉。

还包括一个链文件，以从b37转换。

------

### 6. b36资源: 从b37转换

包括千人基因组项目b36格式的参考序列（human_b36_both.fasta）以及所有转换的VCF文件。refGene track和BAM文件不可用。我们只为这个基因组构建提供数据文件，它可以从我们的master b37库中“轻松”地转换。对于这可能造成的不便表示抱歉。

还包括一个链文件，以从b37转换。