---
layout:     post
title:      HLA分型软件总结
subtitle:   hla学习笔记
date:       2018-01-17
author:     zd200572
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - HLA

---

HLA分型仍然是现在医学的难题，特别是在现在短读长测序依旧盛行的时代。虽然三代测序可有效解决HLA的测序，但现阶段成本较低的依旧是以illumina为首的测序分型。临床下在使用的金标准PCR-SBT技术存在分型不唯一的问题。主流的两家公司的产品，华大的5M panel，illumina的50k pannel，已经能满足临床的使用要求，能将分型做到6位（2*3）以上。一些软件设计是为了从全基因组和全外显子组数据中获得HLA分型；而另一些则是从snp芯片数据（也就是消费级基因检测现阶段主流的芯片，如南方基因、wegene、23魔方等）中获得。下面，我们来一起看看有哪些开源（公开）软件可以实现HLA分型。

# 一、基于WGS、WES、target-seq的软件

## 1. xHLA（2017）

这个软件是人类长寿公司开发，见我的博客：http://www.zd200572.com/2017/09/10/xHLA/

这个软件的独特之处在于其将核酸序列翻译成氨基酸序列进行比对，提高了运行效率，号称减少了硬件使用，但是实际使用体验是巨耗CPU和内存，一个正常的panel样本居然要用上全部的cpu资源几十到上百G内存，最长达两个小时的运行时间。对A、B、C、DPB1、DRB1进行分型。

## 2. HLA-HD（2017）

日本研究所开发，见我的博客：http://www.zd200572.com/2017/12/03/HLA-NGS-treat/

这个软件实际使用下来对内存和cpu的占用还好，我的笔记本双核i3-3120m，12G内存还有余，只是这结果对于覆盖区域较少的数据不友好。可以对classI、ClassII、ClassIII全部进行分型。

## 3. HLAscan（2017）

http://www.genomekorea.com/display/tools/HLAscan 韩国基因研究所发表的，作者十分热情，我询问问题很快给我了邮件回复。

这是韩国团队开发的软件，感觉这个软件效率不够高，我的目标区域测序的数据运行了两天两夜只运行到比对完一个A基因座，应该是我的笔记本太弱了。感觉这个软件用的是穷举法，把所有的等位基因比对一遍，作者说全基因组数据在至强处理器上运行一个小时。

## 4. HLA-PRG-LA（2016）

https://github.com/AlexanderDilthey/HLA-PRG-LA

一个德国科学家开发的软件，他自己也认为这个软件太消耗资源，于是开发了个LA版本的，软件需要编译，比较复杂，没有安装成功。有docker文件，用法也比较复杂，令人困扰。对HLA-A, -B, -C, -DQA1, -DQB1, -DRB1进行分型。

## 5.HLAreporter

一个中国香港的团队开发的，这个软件对测序数据的要求很高，而且，250PE的数据需要切分成2*125的，这一步没有成功。运行结果就是没有结果了。看文献也说有的全外显子测序数据直接会分型失败。

http://paed.hku.hk/genome/software/HLAreporter.zip

## 6. SOAP-HLA

华大基因开发的soap系列软件之一，网上公开的版本在2013年，感觉比较老了，用hg19做参考基因组，使用起来比较简单，对全部基因进行分型，同样需要测序数据覆盖较全面。http://soap.genomics.org.cn/SOAP-HLA.html



## 7. 其他软件

* HLA-VBseq
* Optitype :只对ABC进行分型，据报道准确率较高，开发团队贴心地提供了在线版本。使用效果是对ABC的分型结果不错，目标区域测序数据分析耗时在1小时左右。幸亏有在线版，自行编译安装，bioconda安装和docker都会报错。http://www.epitoolkit.de/root?tool_id=optitype
* ATHLATES: Broad研究所开发，我卡在了安装其依赖的bamtools上，bamtools又依赖于jsongcc，jsongcc安装成功还是不能装，编译报错，也是醉了。
* PHLAT
* HLA-Forest
* Omixon HLA explore：在外显子数目少的情况下分型效果很差，申请了一个30天试用版本。
* illumina HLA Sure Select Assign: 商业产品，没有试用。
* HLAssign:一个德国团队开发的有图形界面的产品，不太了解怎么使用。

# 二、基于SNP芯片

基于snp的分型准确率需要参考人群专一，比如中国北方汉族和中国南方汉族都不能用一个参考数据训练。而且分型的准确率较差，不能具有实用价值，一般只能分到四位（2*2）。

## 1. SNP2HLA（2014）

同样是大名鼎鼎的Broad研究所开发，这个软件需要用到plink和beagle，我对plink格式转换比较疑惑，小数据测试结果里没有分型，不明白呀！http://software.broadinstitute.org/mpg/snp2hla/

## 2.HLA-check(2017)

今年新发表的一款软件，ABC的准确率有所提升，但是会丢弃许多样本。依赖于ShapeIT and IMPUTE2，对这两个软件不甚了解，还没有实际用。https://github.com/mclegrand/HLA-check/

## 3. HIBAG

是bioconductor的一个R包，也比较有应用门槛，还没学会怎么用。

## 4.eHLA

2011年发表的一个较老的软件，还没有测试。

## 5. MAGprediction

http://qge.fhcrc.org/暂未使用。

## 6.HLA-IMP系列

需要在线使用，在线资源均已失效。





我的个人博客：[http://blog.zd200572.com](http://blog.zd200572.com/)和[www.zd200572.com](http://www.zd200572.com/)



