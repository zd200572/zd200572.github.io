---
layout:     post
title:      四十而不惑：DNA测序技术前世今生和未来
subtitle:   zd00572
date:       2017-10-12
author:     zd200572
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
    - 生物信息
    - bioinformatics
    - notes
    - 测序
---
![](http://owxbk335s.bkt.clouddn.com/ngs%2040-1.png)
这篇综述回顾了DNA测序技术发明四十周年以来的发展历程，规模从几个碱基对第一个人类基因组，我们已经见证了多个技术革命和增长，现在获得的百万人和其他多种的基因组。DNA测序技术已被广泛地使用，包括作为一个广阔的分子的计数器。我们预测，从长远来看，DNA测序的影响将可与显微镜相提并论。
## 1.DNA测序技术的历史
![](http://owxbk335s.bkt.clouddn.com/ngs40-2.png)
### 早期测序

最早是胰岛素（蛋白质）和tRNA早于DNA完成了测序。其中，第一个RNA测序用了140kg的酵母测出了76个核苷酸。

### DNA测序技术的发明**

1973年Gilbert和Maxam引物延伸法测定了24个核苷酸，每个核苷酸在耗时一个月。

1976年Sanger和Coulson链终止法和Gilbert和Maxam化学裂解法。

1979年鸟枪法测序

1987年Smith、Hood和Applied Biosystems开发了桑格法荧光测序仪，1000base/d。

1982年Genbank上存储了500,000bases.

1986年Genbank上存储了10,000,000bp.(统计数据见[ https://www.ncbi.nlm.nih.gov/genbank/statistics/](https://www.ncbi.nlm.nih.gov/genbank/statistics/）)）

### 扩大到人类基因组

**1.几个显著进步**：1）从染料标记的引物到染料标记的末端; 2）突变的T7 DNA聚合酶; 3）线性扩增反应；4）基于磁珠的DNA纯化和提取；5）PE双端，双链测序；6）毛细管电泳；7）工业化标准的加入。

**2.软件的开发**：phred，质量度量Q值, phrap, the TIGR assembler and the Celera assembler

**3.测序成本的下降**:2001年一个测序中心可以测10,000,000bp/day. 2004年￥1/（600-700bp).

4.和HGP计划平行进行的私人基因组测序**Craig Venter** and Celera (2001)。

### 大规模平行DNA测序

1.核心是体外扩增产生**每个模板拷贝被测序**，而不是细菌克隆。

2.几种**扩增**方式有polonies，桥式pcr或者滚环扩增（纳米球）。

3.**边合成边测序**的三种方式：1）焦磷酸测序2）使用DNA连接酶的特异性荧光寡核苷酸模板附在顺序的方式3）聚合酶介导下逐步加入荧光标记的脱氧核苷酸（1998, Solexa）

4.第一个NGS测序平台是**454**（2005）, 然后是**Solexa**（35bp PE）。

5.几个NGS平台**454**（Roche收购），**Solexa** ( Illumina收购), **Agencourt**  (Applied Biosystems收购), **Helicos**  (founded by Quake), **Complete Genomics**  (founded by Drmanac华大收购) ， **Ion Torrent** (founded by Rothberg)。

6.**2012年454, SOLiD 和 Helicos停止开发**，illumina成为主流，尽管华大是个潜在挑战者。准确度99.9%，Novaseq可以两天内产生1百亿reads，是HGP计划23G的40倍。

### 单分子实时测序

**1.PacBio**:零模波导孔，大于10k的读长，10%的原始错误率，很低的gc偏好性。

**2.纳米孔测序**：Oxford Nanopore Technologies (ONT)，最长读长可达900K, 便携式，电信号检测，但是错误可能不是随机的。

**3.两者均可检测碱基修饰，甲基化等。**
![](http://owxbk335s.bkt.clouddn.com/ngs40-4.png)
### DNA测序的应用
![](http://owxbk335s.bkt.clouddn.com/ngs40-3.png)
**1.基因组的de novo组装**

（1）遗传图谱（2）物理图谱（3）双端测序，8-10冗余，1/100,000的错误率（4）Celera, 从贪婪算法（phrap and the TIGR ­assembler）到基于图的方法（重叠–布局–­共识）（5）de Bruijn graphs (如 EULER and Velvet)（6）高分子量high molecular weight (HMW)（7）HiC

**2.基因组测序**

1）重测序：Bowtie and Burrows–Wheeler Aligner (**BWA**)数据压缩，**SAMtools** and later **GATK**。

2）几个计划：Genome Aggregation Database ([http://gnomad.broadinstitute.org/](http://gnomad.broadinstitute.org/))

Genomics England ([[https://www.genomicsengland.co.uk/](https://www.genomicsengland.co.uk/)](http://gnomad.broadinstitute.org/))

NHLBI TOPMed (TransOmics for Precision Medicine, [[https://www.nhlbiwgs.org/](https://www.nhlbiwgs.org/)])

### 测序的临床应用

**1.无创产前诊断** non-invasive prenatal testing (NIPT)

**2.WES**： Mendelian and neurodevelopmental disorders

**3.癌症**：靶向治疗、非侵入性诊断和监测ctDNA, cfDNA,发现新的突变位点。

**4.测序仪作为分子计数装置**：RNA-seq取代芯片，TopHat and Cufflinks（[http://enseqlopedia.com/](http://enseqlopedia.com/)）
![](http://owxbk335s.bkt.clouddn.com/ngs40-5.png)
### 宏基因组测序

## DNA测序技术的未来

### 100%基因组，没有任何gap

### 人口规模的测序

### 生物学的发展：单细胞RNA-seq、基因编辑

### 实时、便携式测序仪

### 非常规使用：DNA合成等 

##  DNA测序作为新的显微镜 



