---
layout:     post
title:      Rosalind-18-ORF answer
subtitle:   Open Reading Frames
date:       2017-07-06
author:     zd200572
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - Rosalind
    - 生物信息
    - Bioinformatics
    - Python3
---

#欢迎到我的博客#


最近已经基本上学完了《Python生物信息学数据管理（Managing your Biological Data with Python)》，之前学了一点rosalind（生物信息学练习python的好网站。http://rosalind.info/problems/locations/）的内容，现在继续学习下去。

这是第18题的解答。

'
================================
Open Reading Frames
================================
Problem

Either strand of a DNA double helix can serve as the coding strand for RNA transcription. Hence, a given DNA string implies six total reading frames, or ways in which the same region of DNA can be translated into amino acids: three reading frames result from reading the string itself, whereas three more result from reading its reverse complement.

An open reading frame (ORF) is one which starts from the start codon and ends by stop codon, without any other stop codons in between. Thus, a candidate protein string is derived by translating an open reading frame into amino acids until a stop codon is reached.

Given: A DNA string ss of length at most 1 kbp in FASTA format.

Return: Every distinct candidate protein string that can be translated from ORFs of ss. Strings can be returned in any order.

Sample Dataset

'>Rosalind_99
AGCCATGTAGCTAACTCAGGTTACATGGGGATGACCCCGCGACTTGGATTAGAGTCTCTTTTGGAATAAGCCTGAATGATCCGAGTAGCATCTCAG
Sample Output

MLLGSFRLIPKETLIQVAGSSPCNLS
M
MGMTPRLGLESLLE
MTPRLGLESLLE
'

[https://github.com/zd200572/rosalind16-/blob/master/18-ORF.py](https://github.com/zd200572/rosalind16-/blob/master/18-ORF.py)