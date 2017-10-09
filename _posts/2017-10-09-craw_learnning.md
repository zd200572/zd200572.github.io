---
layout:     post
title:      爬虫小试-0217影响因子表
subtitle:   zd00572
date:       2017-10-09
author:     zd200572
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
    - 生物信息
    - bioinformatics
    - notes
    - Python3
---
> 题目来源于生信技能树论坛，参考了几个帖子。
> [http://www.biotrainee.com/thread-1695-1-1.html](http://www.biotrainee.com/thread-1695-1-1.html)
> [http://www.biotrainee.com/thread-1316-1-1.html](http://www.biotrainee.com/thread-1316-1-1.html)
> 
比如这个最简单的，表格爬取：
http://www.letpub.com.cn/index.p ... r=¤tpage=1000
http://www.letpub.com.cn/index.p ... tter=¤tpage=3 
http://www.letpub.com.cn/index.p ... tter=¤tpage=2 
http://www.letpub.com.cn/index.p ... tter=¤tpage=1 
规律很简单，就是url从1增加到1000即可，很简单的循环！
每一个页面只有一个表格，所以很容易提取，用python,perl,R都可以 
截止2017年，一共收录期刊：9991份
试试看吧

里边最重要的就是正则表达式了，另外就是把想要的内容分离出来，这是个很简单的爬虫，我的代码也很初级，仍需继续努力学习！

遇到的问题有：1、网络连接被切断，估计是没有进行伪装成浏览器的原因；2、才开始正则表达式影响因子中有两位数的，没有考虑；3、有的被除名的标签不一样，导致有影响因子（0.000）没有杂志名。
我的代码如下：

    import requests
    import re
    import time
    
    fout = open('ifs.csv', 'w')
    
    
    for i in range(79, 1001):
	    j_name = []
    	ifs = []
    	dict = {}
    	url = 'http://www.letpub.com.cn/index.php?page=journalapp&fieldtag=&firstletter=&currentpage=%s' % i
    	content = requests.get(url).text
    	#print(content)
    	re1 = re.compile(r'<a style="color:#0099FF; font-size:12px; font-weight:bold; .*?;" .*?&page=journalapp&view=detail" target="_blank">.*?</a><br><br>')
    	re2 = re.compile(r'<td style="border:1px #DDD solid; border-collapse:collapse; text-align:left; padding:8px 8px 8px 8px;">\d+\.\d+</td>')
    	#re3 = re.compile(r'')
    	journal_name = re1.findall(content)
    
    	
    	for a in journal_name:
    		name = a.split('</a>')[0].split('>')[1]
    		j_name.append(name)
    		dict[name] = ''
    	iF = re2.findall(content)
    	for a in iF:
    		ifa = a.split('</td>')[0].split('>')[1]
    		#if ifa != '0.000':
    		ifs.append(ifa)
    	print(ifs)
    
    	j = 0
    	print(len(dict))
    	for c in dict.keys():
    		#print(c)
    
    		if j < len(dict):
    			dict[c] = ifs[j]
    			j += 1
    		fout.write(str(c) + ',' + str(dict[c]) + '\n')
    	time.sleep(6)
	#break
    fout.close()








