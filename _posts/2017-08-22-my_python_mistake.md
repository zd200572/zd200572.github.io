---
layout:     post
title:      python return 翻车记
subtitle:   zd00572
date:       2017-08-22
author:     zd200572
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
    - IT
    - python
    - Notes
---
不是最近在学**think Python**嘛，失败的是已经完全按照作者答案的算法改写了程序，竟然还是得到的结果不一样。一句一句地分析，花了很长时间，才发现是return语句用错了，放在了程序中间，导致程序提前结束，后边的语句不可能执行的，也是醉了。
    def is_pallindrome_number():
    	list = []
    	for i in range(198888, 200000):
    		#print(i)
    		j = str(i)
    		if j[::-1][:4] == j[2:]:
    			#print(i)
    			
    			if str(i + 1)[::-1][:5] == str(i + 1)[1:]:
    				#print(i)
    				if str(i + 2)[::-1][1:5] == str(i + 2)[1:5]:
    					#print(i)
    					
    					if str(i + 3)[::-1] == str(i + 3):
    						#print(i)
    						list.append(i)
							#这是才开始我的return语句位置return list
    	return list 

**作者的代码：**
    from __future__ import print_function, division
    
    
    def has_palindrome(i, start, length):
    """Checks if the string representation of i has a palindrome.
    
    i: integer
    start: where in the string to start
    length: length of the palindrome to check for
    """
    s = str(i)[start:start+length]
    return s[::-1] == s
    
    
    def check(i):
    """Checks if the integer (i) has the desired properties.
    
    i: int
    """
    return (has_palindrome(i, 2, 4) and
    has_palindrome(i+1, 1, 5) and
    has_palindrome(i+2, 1, 4) and
    has_palindrome(i+3, 0, 6))
    
    
    def check_all():
    """Enumerate the six-digit numbers and print any winners.
    """
    i = 100000
    while i <= 999996:
    if check(i):
    print(i)
    i = i + 1
    
    
    print('The following are the possible odometer readings:')
    check_all()
    print()