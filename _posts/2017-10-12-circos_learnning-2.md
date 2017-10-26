---
layout:     post
title:      circos学习笔记（二）
subtitle:   zd00572
date:       2017-10-12
author:     zd200572
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
    - 生物信息
    - bioinformatics
    - notes
    - circos
---
今天用自己的数据做了一下circos圈图，当然，是在生信媛那三篇教程的基础之上（[http://mp.weixin.qq.com/s/qXDlKf7ut8QF2c5_0hiKpA](http://mp.weixin.qq.com/s/qXDlKf7ut8QF2c5_0hiKpA)[http://www.biotrainee.com/thread-755-1-1.html](http://www.biotrainee.com/thread-755-1-1.html)），修改了部分参数。其实，主要是数据格式的处理过程，我采用python脚本处理的，处理起来感觉还好，没有多少难度，因为大部分的数据是提取两列而已，不需要我进行更复杂的处理，更复杂的处理估计也有软件解决，不需要我造轮子了。

**下面是我的过程记录：**

## 1.contig大小、起始位点的配置文件

我的原始数据来自美吉生物的结果，有一个assemble文件夹里边有一个fasta_name.txt，有这些统计信息，想起来了，我个我是用一个shell命令获得的，但是这些信息都在那个组装好的基因组文件里。

    cat d-1.Contigs.fna | grep ^'>' > fasta_name.txt
![](http://owxbk335s.bkt.clouddn.com/d1-contig.png)

把数据处理成circos格式，一个python脚本解决（虽然python水平蹩脚，但是能解决小问题了）：

    fin = open('fasta_name.txt')
    contig = ''
    start = 0
    end = 0
    dict = {}
    for line in fin:
    	li = []
    	contig = line.strip().split(' ')[0].split('>')[1]
    	dict[contig] = ''
    	li.append(start)
    	end += int(line.strip().split('=')[1].split('   ')[0])
    	li.append(end)
    	dict[contig] = li
    	start = end  
    #print(dict)
    
    fout = open('tRNA.gff', 'w')
    fin2 = open('G:\\Users\\shenyou\\Desktop\\ddm-1\\tRNA\\tRNA.gff')
    for line in fin2:
    	#print(line)
    	contig = line.strip().split('	')[0].strip()
    	print(contig)
    	start1 = int(line.strip().split('	')[2])
    	print(start1)
    	end1 = int(line.strip().split('	')[3])
    	print(end1)
    	#break
    	start1 += dict[contig][0]
    	end1 += dict[contig][0]
    	fout.write(contig + ' ' + str(start1) + ' ' + str(end1) + '\n')
    fout.close()

## 2.基因注释数据的处理

上面获得了，contig的数据，基本的环就形成了，然后再按生信媛的教程加上刻度不表。下面我选择了测序数据报告里的tRNA、rRNA和基因的预测数据，进行了处理，处理方式都是一样的，可以用一个脚本改改参数解决。主要处理方式就是，把那个在每个contig上的相对刻度转化为基因组的绝对刻度，我是字典解决问题的。脚本如下：

    fin = open('fasta_name.txt')
    contig = ''
    start = 0
    end = 0
    dict = {}
    for line in fin:
    	li = []
    	contig = line.strip().split(' ')[0].split('>')[1]
    	dict[contig] = ''
    	li.append(start)
    	end += int(line.strip().split('=')[1].split('   ')[0])
    	li.append(end)
    	dict[contig] = li
    	start = end  
    #print(dict)
    
    fout = open('predict.gff', 'w')
    fin1 = open('G:\\Users\\shenyou\\Desktop\\ddm-1\\predict\\ddm-1.ffn')
    for line in fin1:
    	if line.startswith('>'):
    		contig = line.strip().split(' ')[3]
    		start1 = int(line.strip().split(' ')[4])
    		end1 = int(line.strip().split(' ')[5])
    		start1 += dict[contig][0]
    		end1 += dict[contig][0]
    		fout.write(contig + ' ' + str(start1) + ' ' + str(end1) + '\n')
    fout.close()

## 3.gc含量的获得、

其实，我个步骤对于我来说是最难的，我试图找一个软件来解决，但是碍于自己知识不足，都搜不到相关信息，只有自己造轮子了，写了一个小脚本竟然解决问题了，有点成就感。主要思路就是按生信媛教程里的数据格式，每1000bp计算一次gc含量，对了，还有偏移可以用，由于不清楚正负链的情况，就一锅端了。脚本如下：

    fin1 = open('fasta_name.txt')
    contig = ''
    start = 0
    end = 0
    dict = {}
    for line in fin1:
    	li = []
    	contig = line.strip().split(' ')[0].split('>')[1]
    	dict[contig] = ''
    	li.append(start)
    	end += int(line.strip().split('=')[1].split('   ')[0])
    	li.append(end)
    	dict[contig] = li
    	start = end  
    #print(dict)
    
    i = 1
    fin = open('G:\\Users\\shenyou\\Desktop\\ddm-1\\assembly\\ddm-1.Contigs.fna')
    seq = ''
    di = {}
    flag = 0
    #sequence = ''
    for line in fin:
    	if line.startswith('>'):
    		if seq != '':
    			di[contig] = seq
    			#print(contig, di[contig][:10])
    		contig = line.strip().split(' ')[0].split('>')[1]
    		#print(contig)
    		i += 1
    		#break
    		di[contig] = ''
    		seq= ''
    	else:
    		seq += line.strip()
    		#sequence += line.strip()
    
    seq_gc = 0.6537235194562051
    #print(di.keys())
    
    fout = open('gc.txt', 'w')
    for a in di.keys():
    	#print(a)
    	j = 0
    	for j in range(int(len(di[a]) / 1000) - 1):
    		if j == 0:
    			if len(di[a]) >= 1000:
    				#print(str(di[a]))
    				seqi_gc = (di[a][0:1000].count('G') + di[a][0:1000].count('C')) / 1000
    				start = dict[a][0] + 1
    				end = 1000 + dict[a][0]
    			elif len(di[a]) < 1000:
    				#print(str(di[a]))
    				seqi_gc = (di[a][0:len(di[a])].count('G') + di[a][0:len(di[a])].count('C')) / len(di[a])
    				start = dict[a][0] + 1
    				end = len(di[a]) + dict[a][0]
    		elif 1 <= (j + 1) < int(len(di[a]) / 1000):
    			#print(str(di[a]))
    			seqi_gc = (di[a][j*1000:(j + 1)*1000].count('G') + di[a][j*1000:(j + 1)*1000].count('C')) / 1000
    			start = j*1000 + dict[a][0] + 1
    			end = (j + 1)*1000 + dict[a][0]
    		elif (j + 1) == int(len(di[a]) / 1000):
    			#print(str(di[a]))
    			seqi_gc = (di[a][j*1000:len(di[a])].count('G') + di[a][j*1000:len(di[a])].count('C')) / (len(di[a]) - j*1000)
    			start = j*1000 + dict[a][0] + 1
    			end = len(di[a]) + dict[a][0]
    		print(start, end)
    		fout.write(str(a) + ' ' + str(start) + ' ' + str(end) + ' ' + str(seqi_gc) + '\n')
    		j += 1
    	#break
    fout.close()
    
## 4.我的配置文件总览

根据教程，我的配置文件如下，没有出现报错的情况，但是想要掌握这个画图，还是要下很多很多功夫的。

    <<include etc/colors_fonts_patterns.conf>>
    <image>
    <<include etc/image.conf>>
    </image>
    karyotype = karyotype.txt
    chromosomes_units = 100000
    chromosomes_display_default = yes
    <ideogram>
    <spacing>
    default = 0.005r
    </spacing>
    radius = 0.80r
    thickness = 6p
    fill = yes
    fill_color = deepskyblue
    stroke_color = black
    stroke_thickness = 1p
    show_label = yes
    label_font = light
    label_radius = 1r + 110p
    label_size = 30
    label_parallel = yes
    </ideogram>
    <<include etc/housekeeping.conf>>
    
    show_ticks = yes
    show_tick_labels = yes
    <ticks>
    skip_first_label = no
    skip_last_label = no
    radius = dims(ideogram,radius_outer)
    color = black
    thickness = 2p
    size = 30p
    multiplier = 1e-6
    format = %.2f
    <tick>
    spacing = 20000b
    size = 10p
    show_label = no
    thickness = 3p
    </tick>
    <tick>
    spacing = 100000b
    size = 20p
    show_label = yes
    label_size = 25p
    label_offset = 10p
    format = %.2f
    </tick>
    </ticks>
    
    <highlights>
    z = 0
    <highlight>
    file = predict.gff
    r0 = 0.90r
    r1 = 0.99r
    fill_color = 169,169,169
    </highlight>
    <highlight>
    file = tRNA.gff
    r0 = 0.81r
    r1 = 0.90r
    fill_color = 169,169,169
    </highlight>
    <highlight>
    file = rRNA.gff
    r0 = 0.27r
    r1 = 0.36r
    </highlight>
    </highlights>
    
    <plots>
    type = line
    thickness = 1p
    <plot>
    z = 2
    max_gap = 0u
    file = gc.txt
    color = red
    fill_color = red
    r0 = 0.69r
    r1 = 0.78r
    orientation = out
    </plot>
    
    <plot>
    z = 2
    max_gap = 0u
    file = gc_a_m.txt
    color = aquamarine
    fill_color = aquamarine
    r0 = 0.48r
    r1 = 0.57r
    orientation = out
    </plot>
    
    </plots>

## 6.我的图

最基础的图画好了，凑活着看了，没想到第一次画就能画成这样，感谢教程。

![](http://owxbk335s.bkt.clouddn.com/1circos.png)