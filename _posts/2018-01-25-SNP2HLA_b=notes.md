---
layout:     post
title:      SNP2HLA软件使笔记
subtitle:   HLA学习笔记
date:       2018-01-25
author:     zd200572
header-img: img/post-bg-alitrip.jpg
catalog: true
tags:
    - HLA

---



最近在尝试用芯片数据进行HLA分型，做做笔记。

# 1. 基本概念学习

* **Imputation**：中文名称叫做基因型填充，是根据已知的基因分型数据对未分型的数据进行预测。代表软件有MACH和IMPUTE。
* **plink**:是基因型--表型分析软件，其ped文件格式前六列是家系、个体、父亲、母亲、性别（1男/2女/0其他）
* **Haploview**：用于单倍型分析的软件。
* **HLA区域特点**：强连锁不平衡和高度多态性。

# 2. SNP2HLA的使用

## 2.1 软件介绍

见http://www.zd200572.com/2018/01/17/HLA-software-review/

## 2.2 涉及中国人的软件的几个参考数据集的情况

* **CHB+JP**:是Hapmap计划中中国人群的数据，中国人54人。
* **Pan-Asia**：530人，其中，中国人100多人。HLA区域：2142SNPs
* **HAN.MHC**：100869人，全部为中国人。HLA区域：3756SNPs

能使用最后一个参考数据集进行分型是最好的，但是，最后一个数据公开不全，我的知识水平难以解决。

## 2.3 软件使用方法和结果提取

使用方法见官方文档，很简单的一个命令。

我一度很困惑，结果运行完之后没有一个直观的结果，直到我使用表格软件进行HLA关键字的筛选，发现P代表着候选基因型的意思（bgl.phased文件）。但是，每两列是一个样本，每列是其一个单体型，手动难以挑出，于是想写几句小脚本解决，以三脚猫水平费了九年二虎之力终于将其解决。主要想法就是用一个函数获得样品id,在第二行，建立一个字典，存储样本名和列序号。然后用另一个函数获取结果并对应样本写入文件。中间发现由于两列的键值相同，字典只是样本号和第二个单体型列号的对应关系，还好，不复杂，一次检查两个，减去1即可，还比原来提高了效率。代码如下：

```python
########get##result##from##SNP2HLA####################


def get_sample_id(fin):
	with open(fin) as f:
		HLA_type = {}
		hla_id = {}
		i = 0
		for line in f:
			if i == 1:
				#print(line)
				#break
				j = 2
				#print(len(line.strip().split(' ')))
				for j in range(2, len(line.strip().split(' '))):
					#print(j)
					sample_id = line.strip().split(' ')[j]
					#print(sample_id)
					HLA_type[sample_id] = []
					hla_id[sample_id] = j
			i += 1
		#print(hla_id)
	return HLA_type, hla_id


def get_HLA_typing_result(fin, HLA_type, hla_id):
	#print(hla_id)
	new_dict = {v:k for k,v in hla_id.items()} 
	fout = open('HLA-result.txt', 'w')
	i = 0
	j = 0
	for j in hla_id.values(): #range(2, len(HLA_type)):
		with open(fin) as f:
			if j in hla_id.values():
				print(j, new_dict[j])
				#break
				fout.write(str(new_dict.get(j)) + '\t')
			#print(j)
			#HLA_allele = []
			for line in f:
				'''
				if i == 1:
					#print(line)
					#break
					#print(len(line.strip().split(' ')))
					for j in range(2, len(line.strip().split(' '))):
						sample_id = line.strip().split(' ')[j]
						#print(sample_id)
						HLA_type[sample_id] = []
						hla_id[sample_id] = j
				'''
				sub_line = line.strip().split(' ')
				#if i <= 16:
				#	print(sub_line[1])
				#break
				#print(j)
				if 'HLA' in sub_line[1] and sub_line[j - 1] == 'P':
					#print(sub_line[1])
					fout.write('\t' + sub_line[1])
					#HLA_type[hla_id.get(j)].append(sub_line[1])
				if 'HLA' in sub_line[1] and sub_line[j] == 'P':
					fout.write('\t' + sub_line[1])
					#print(sub_line[1])
					#HLA_type[hla_id.get(j)].append(sub_line[1])
					#print(hla_id.get(j), HLA_allele)
				i += 1
			#HLA_type[hla_id.get(j)] = HLA_allele
		
					#break
							
					
			#j += 1
			fout.write('\n')
			#print(HLA_type)
	fout.close()



HLA_type, hla_id = get_sample_id('23s.bgl.phased')
get_HLA_typing_result('23s.bgl.phased', HLA_type, hla_id)
```

其实也可以以另一种思路来，以列为处理单元，去对应每一个行，或许效率更高。



我的个人博客：[http://blog.zd200572.com](http://blog.zd200572.com/)和[www.zd200572.com](http://www.zd200572.com/)



