---
layout:     post
title:      ascp下载ebi ncbi数据库大文件
subtitle:   zd00572
date:       2017-08-09
author:     zd200572
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
    - 生物信息
    - 转录组
    - bioinformatics
    - Notes
---
# ascp下载ebi ncbi数据库大文件
在技能树论坛里看到有人说ascp可以下载宽带满速，就百度了一下，但是发现ncbi的正常可用，ebi的已经不能用了，所以更新一下。
## ebi 千人基因组计划数据下载代码   ##

     ascp -i asperaweb_id_dsa.openssh -Tr -Q -l 6M -P33001 -L- -k1 era-fasp@fasp.sra.ebi.ac.uk:/vol1/fastq/ERR262/ERR262997/ERR262997_1.fastq.gz H:\

## ncbi ##

    anonftp@ftp-private.ncbi.nlm.nih.gov://sra/sra-instant/reads/ByExp/sra/SRX/SRX248/SRX248556/SRR771547/SRR771547.sra

下载速度真的真的好快！！！宽带满速是真的，这技术，比迅雷更牛呀！

附上说明网页：
http://www.internationalgenome.org/faq/how-download-files-using-aspera
参考：
http://www.bbioo.com/lifesciences/40-116614-1.html
