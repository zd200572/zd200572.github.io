---
layout:     post
title:      Cytoscape学习笔记
subtitle:   zd00572
date:       2017-10-27
author:     zd200572
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
    - 生物信息
    - 软件
    - Cytoscape
    - Notes
---
坚持学习！我是在win下安装使用的，从南京图书馆借了本《生物信息学理论与技术》，第二章介绍的是Cytoscape，决定尝试一下。

# 1.先学习一下Cytoscape

Cytoscape是一款图形化显示网络并进行分析和编辑的软件，它支持多种网络描述格式，也可以用以Tab制表符分隔的文本文档或Microsoft Excel文件作为输入，或者利用软件本身的编辑器模块直接构建网络。

Cytoscape还能够为网络添加丰富的注释信息，并且可以利用自身以及第三方开发的大量功能插件，针对网络问题进行深入分析。　Cytoscape对非盈利性客户免费。

内容来自百度百科：https://baike.baidu.com/item/CytoScape/2154603?fr=aladdin

软件官网：[www.**cytoscape**.org/](http://www.baidu.com/link?url=seFMx9veKnQavh_poNAmXd-QHsp1nOL-vUOCti9lmAbf_xmoSf9-5Apu0ZCCTAwU)

# 2.从excel表格创建网络

书中给了示例数据，我把它手工录入了excel，放在了github上。

![](http://owxbk335s.bkt.clouddn.com/cytoscape-excel.png)

File--import-Network-File选中MAPK.xls，不像书中所说要自己调整，新版的软件已经比较智能，直接生成了书中的环形图。

![](http://owxbk335s.bkt.clouddn.com/cytoscape-import.png)

选中节点，右键Edit--Bypass Style--set Bypass to Selected Nodes，这样会调出一个控制面板，现在软件更方便易用了，几乎所有的处理工作都在这个面板里可以设置好了。

![](http://owxbk335s.bkt.clouddn.com/cytoscape-set%20node%20color.png)

![](http://owxbk335s.bkt.clouddn.com/cytoscape-excel-final.png)

还可以选中一个结点，对其进行在线扩展：External Links--Ontology--Gene-Ontology(by name)，这是进行EMBL-EBI数据库的查询;External Links--Pathway Database--KEGG Pathway等等。

# 3.Cytoscape插件

## 1）Agilent Literature Search

从标题可以看出这是一个文献检索相关的工具，首先是安装Apps-App Manager--先择这个插件即可。然后使用就从Apps--Agilent Literature Search，就可以使用了，在Terms输入Alzheimer， Context输入IL1，检索，就出来了结果，结果就是一个网络图，好玩吧！

![](http://owxbk335s.bkt.clouddn.com/cytoscape-agilent.png)

然后，选中一个结点，还可以查找文献证据，Evidence from literature--show sentence from literature，就会出现文献中的句子，神奇呀！

![](http://owxbk335s.bkt.clouddn.com/ctoscape-agi-sentences.png)

## 2）CyKEGGParser

同样的方法安装好这个插件，好像文件有点大，还是网络问题，下了有两分钟的。

Apps--CyKEGGParser--Load KGML--KEGG web Load task，由于我没有文件，就从网上下载了，又是好方便，网络图直接就有了，简直是神器。下载的是has04750，书中hsa应该是写错了，找不到。 

![](http://owxbk335s.bkt.clouddn.com/cykeggparser-1.png)

## 3) APID2NET

这是个进行PPI分析的工具。基因的最终产物包括蛋白质，蛋白质通过互相作用（PPI）行使功能。这个安装要用2.6版本的软件，估计是没有更新，所以就不试了。

## 4）CytoCluster

不同于前边3个生成网络的，这个是做网络分析的。但是比较多的内容涉及算法的，我表示看不懂。我就简单了解了一下。

## 5) JEPETTO

整合型基因组分析工具，相互作用关系、信号通路和生物过程等数据。安装还是一样的方法。

使用：Apps--JEPETTO--Enrichment Analysis(富集分析)，用书中所列的基因列表，即可获得富集分析的结果。富集分析的概念查了下，放在这里： 基因富集分析是分析基因表达信息的一种方法，富集是指将基因按照先验知识，也就是基因组注释信息进行分类。

![](http://owxbk335s.bkt.clouddn.com/cytoscape-JEPETTO.png)

## 6）GeneMANIA

其可以独立地进行网络构建和分析，在基因数量较多时，可以使用其在线工具进行。其分析的基因与基因的关系有共表达（GEO)、蛋白相互作用（PPI来自BioGRID和Pathway Commons）、基因相互作用（BioGRID)、蛋白共享结构域（InterPro、SMART和Pfam）和共定位以及信号通路（Reactome和Biocyc）。还包括预测关系和基因表型关系。官网：www.geneminia.org

书中只介绍这个插件的在线使用情况。

好，今天的cytoscape学习就先到这里。

