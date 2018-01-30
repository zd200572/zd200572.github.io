---
layout:     post
title:      使用Pacbio SMRT测序进行HLA分型
subtitle:   HLA学习笔记
date:       2018-01-30
author:     zd200572
header-img: img/post-bg-alitrip.jpg
catalog: true
tags:
    - HLA

---



今天在Pharmacogenomics上读到一篇文章，是讲关于用Pacbio公司的测序技术进行HLA分型的，学习一下方法。文章题目是：Construction of full-length Japanese reference panel of class I HLA genes with single-molecule, real-time sequencing翻译一下应该是**使用单分子实时测序构建日本人HLA一类基因参考集**

作者是日本东北大学的研究团队，当我打开日本东北大学的主页，瞬间震惊了，東北大学四个大字在校徽上，要不是下面的英文名，真的以为是中国东北大学呢，有图为证。

![](http://nagasakilab.csml.org/en/wp-content/uploads/2014/03/header_en2.png)

# 1.摘要

HLA基因复合体在人种间相差极其大，它在器官和造血干细胞移植方面又特别重要，而且许多疾病与不同的HLA等位基因型相关。研究人员从1070个全基因组测序数据(1KJPN)中构建了一个包含208个日本人的HLA一类基因参考集(ToMMo HLA panel)。对于高质量的等位基因重建，开发了一个PSARP（引物-分离组装和优化？）流程，使用了SMRT测序和短读长测序。这个基因参考集包括139个等位基因，均来自已知的IPD-IMGT/HLA 数据库，包含40个新变异，覆盖了1KJPN中大于96.5%的等位基因多样性。这些新的序列对高分辨率HLA分型、遗传相关性研究和顺式调控元件有重要意义。

# 2.简介

这里的文字大概每篇文章差不多，摘录几个名词和句子学习。

* graft-versus-host：移植物抗宿主
* hepatitis C：丙肝
* narcolepsy：发作性睡病
* serological：血清学的
* hampered：阻碍

# 3.材料和方法

* 从WGS数据中提取HLA基因型选用的分析软件是**HLA-VBseq**。
* **PCR产物测序数据的初始分析**：AmpliconAnalysis（包含在SMRT analysis中，默认参数）把样品的测序数据分开--BWA-MEM比对IPD-IMGT/HLA中的序列--A、B、C和H。
* **生信方法--PSARP**：包含三个部分，**a)**SMRT测序的HLA等位基因型组装,**b)**HLA等位基因型的精炼，**c)**低可信基因的过滤。
* **源代码**：http://nagasakilab.csml.org/data/psarp_scripts.zip





**我的**个人博客：[http://blog.zd200572.com](http://blog.zd200572.com/)和[www.zd200572.com](http://www.zd200572.com/)



