---
layout:     post
title:      科研狗词云绘制代码注释
subtitle:   微生物学习笔记
date:       2018-04-26
author:     zd200572
header-img: img/post-bg-alitrip.jpg
catalog: true
tags:
    - R

---



还是科研狗R绘图学习小组的内容，由于尝试加入没有成功，决定跟着学，因为他们在做一些有趣的实用的事情，即使收集代码，稍微改下就能直接使用，很有价值。

> http://group.keyangou.com/RGraph
>
> 第二部分：R语言文本分析及数据分析应用
>
> 1.        R语言访问Pubmed接口获得2016年CELL杂志发表文章数据
>
> 2.        R语言将所获数据存储在mysql数据库
>
> 3.        R语言读取mysql数据文件进行分词并存储
>
> 4.        R语言绘制CELL词汇云
>
> 5.        R语言对CELL词汇进行自定义分析
>
> 6.        R语言中文分词
>
> 7.        R语言获得5000本期刊近5年的影响因子以及绘图
>
> 8.        R语言找出5000本期刊中影响因子上升最快前10名和下降最快前10名以及最稳定的前10名

```R
#任务1
library(RMySQL)
#数据库连接删除函数，每个任务之前最好先清理所有的连接，调用此函数就可以
killDbConnections <- function () {
  all_cons <- dbListConnections(MySQL())
  print(all_cons)
  for(con in all_cons)
    +  dbDisconnect(con)
  print(paste(length(all_cons), " connections killed."))
}#依旧是那个可以清理与数据库链接的函数
killDbConnections()
#创建数据库连接  
con <- dbConnect(MySQL(),host="localhost",dbname="rdb2",user="root",password="")
dbSendQuery(con,'SET NAMES utf8')
rs <- dbSendQuery(con, "SELECT * FROM article WHERE isdone=1")#选中isdone=1的代码，估计就是有内容的。
#涉及到定义函数的学习得比较吃力了，没有相关经验，努力学习呀！
words = data.frame(word=c(), freq = c())#创建一个数据框
while (!dbHasCompleted(rs)) {
  chunk <- dbFetch(rs, 10)
  #chunk[,4]为title, #chunk[,5]为abstract
  count=nrow(chunk)
  cnt=1
  while(cnt<=count){
    str = gsub("[[:punct:]]", "", tolower(chunk[cnt,5])) 
    temp = as.vector(unlist(strsplit(str, split = " ")))
    temp_len = length(temp)
    cnt2 = 1
    while(cnt2 <= temp_len){
if(temp[cnt2] %in% words$word){
    words[words$word == temp[cnt2],]$freq = words[words$word == temp[cnt2],]$freq+1
      }
else{
        words = rbind(words,data.frame(word=c(temp[cnt2]),freq=c(1)))
      }
      cnt2 = cnt2+1
    }
    cnt = cnt +1
  }
}
head(words)
  
  
#任务2
library(wordcloud2)
wordcloud2(words[0:1000,]) 
  
#任务3
#按照freq的降序排列
new_words = words[order(words$freq,decreasing=T),]
#去掉一些定冠词等 of and the
del_word = c('not','two','other','during','of','it','may','the','and','in','to','a','that','is','for','by','with','we','are','an','this','these','as','from','which','at','their','have','or','our','its','but','how','be','as','here','on','can','into','data','between','both','also')
words2 =words[which(!(words$word %in% del_word)),]
wordcloud2(words2)#这个包用法很easy嘛，直接调用就好。
```

![http://image.sciencenet.cn/home/201804/26/161613peozd1vf61zeed4z.png](http://image.sciencenet.cn/home/201804/26/161613peozd1vf61zeed4z.png)

**我的个人博客 **：[http://blog.zd200572.com](http://blog.zd200572.com/)和[www.zd200572.com](http://www.zd200572.com/)



