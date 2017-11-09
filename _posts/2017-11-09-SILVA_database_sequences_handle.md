---
layout:     post
title:      SILVA数据库全库下载序列的处理
subtitle:   处理用于QPCR引物设计的16S序列
date:       2017-11-09
author:     zd200572
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - Rosalind
    - 生物信息
    - Bioinformatics
    - SILVA
---

最近在做肠道微生物的课题，搜索得知SILVA数据库是最近更新而且用的最多的，看网上的教程把其全库的序列下载了下来，没有比对的有200多兆，比对完的超过三个G，参考的那个微信公众号文章说只需要下载没有比对的，我还不信邪，把两个都下载下来了，一个解压后有3G，另一个有76g多，实在是难以处理，3g多的还勉强可以操作，于是就一小的文件做了筛选。

筛选用的是我刚入门的python，虽然水平挺菜，但是至少能用，水平也或许制约这我难以处理76g的文件。贴上我的一段筛选代码，及其简单，都没有什么复杂结构，水平啊！就是从中筛选出一个门或者属/种的16S序列。

```python
fin = open('current_Bacteria_unaligned.fa')
fout = open('Actinobacteria.fasta', 'w')
phylum = ''
dict = set()
i = 1
flag = 0
for line in fin:
	if line.startswith('>'):
		flag = 0
		#phylum = line.strip().split(';')[-2]
		if 'Actinobacteria' in line:
		#if phylum == 'Akkermansia':
			flag = 1
			fout.write(line)
			#print(line, i)
			i += 1
		#break
		#dict.add(phylum)
		
	elif flag == 1:
		fout.write(line)
#print(dict)
print(i)
fout.close()

```

筛选完后发现太多了，特别是门，有几十万条，于是就再精选一下，把门中每个属只留一个，瞬间就变成千条左右了。

```python
fin = open('Actinobacteria-filter.fasta')
fout = open('Actinobacteria-filter-1000.fasta', 'w')
phylum = ''
genusdict = {}
genus = ''
i = 0
flag = 0
for line in fin:
	if line.startswith('>'):
		flag = 0
		#if len(line.strip().split(';')) < 13:
		#	continue
		#else:
		genus = line.strip().split(';')[-2]
		#print(genus)
		if genus not in genusdict.keys():
			flag = 1
			genusdict[genus] = ''
			fout.write(line)
		else:
			continue
	elif flag == 1:
		fout.write(line)
	#break
print(len(genusdict))
fout.close()
```

好了，这样差不多就能愉快地比对找保守区域设计引物了。

|         | 菌门/属、种                               | 总条数    | 筛选后（每属一条） |
| ------- | ------------------------------------ | ------ | --------- |
| 厚壁菌门    | Firmicutes                           | 775435 | 2642      |
| 变形菌门    | Proteobacteria                       | 936216 | 1121      |
| 拟杆菌门菌   | Bacteroidetes                        | 396435 | 316       |
| 放线菌门    | Actinobacteria                       | 362892 | 381       |
| 阿克曼氏菌属  | Akkermansia                          | 2777   |           |
| 普拉梭菌    | *Faecalibacterium prausnitzii***     | 340    |           |
| 解木聚糖拟杆菌 | *Bacteroides xylanisolvens***        | 7      |           |
| 瑞士乳杆菌   | *Lactobacillus helveticus***         | 1321   |           |
| 费氏丙酸杆菌  | *Propionibacterium freudenreichii*** | 18     |           |
| 厌氧球菌属   | *Anaerotruncus colihominis***        | 3      |           |
| 一致粪球菌   | Coprococcus eutactus                 | 2      |           |
|         | *Escherichia albertii***             | 78     |           |
| 普通拟杆菌   | *Bacteroides vulgatus***             | 35     |           |
| 脆弱拟杆菌   | *Bacteroides ovatus***               | 32     |           |
| 迟缓埃格特菌  | Eggerthella lenta                    | 28     |           |
| 罗斯氏菌属   | Roseburia                            | 5905   |           |

