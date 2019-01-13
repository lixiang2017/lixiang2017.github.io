---
title: Calculate Entropy and Divergence
date: 2018-07-27 14:32:53
categories: python
tags: [nlp, ml]
---

任意摘录一段文字，统计这段文字中所有字符的相对频率。假设这些相对频率就是这些字符的概率，请计算其分布的熵。按上述同样的方法计算字符分布的概率，然后计算两段文字中字符分布的 KL 距离。

考虑到汉字总数较多，英文单词也很多；需要大量的数据才有参考意义。所以只是对英文字符进行处理。程序中数据makefile和readme.md来自工作中项目的两个文本文件。真实情况中可能两段文字中所包含的字符不完全相同，所以程序中采用两段文字中共有的字符进行计算KL距离。

```python
#! /usr/bin/python
# function : calculate the entropy and the divergence of two files 
# date     : 2018/6/1
# author   : lixiang

import csv
import math

count = {}
prop = {}
p_count = {}
p_prop = {}
q_count = {}
q_prop = {}

def calc_entropy(file_name):
    H = 0
#   file_name = raw_input("Please input the file name: ")
    csv_reader = csv.reader(open(file_name))
    for row in csv_reader:
#       print row
        for c in str(row):
            if count.has_key(c):
                count[c] += 1
            else:
                count[c] = 1

    del count['[']
    del count[']']
    if count.has_key(' '):
        del count[' ']
    if count.has_key("'"):
        del count["'"]

#   print count
    keys = count.keys()
    print "keys : ", keys
    values =  count.values()
    print "values : ", values

    total = sum(count.values())
    print "Total characters number : ", total

    for c in keys:
        prop[c] = count[c] * 0.1 / total
        H += -1.0 * prop[c] * math.log(prop[c], 2)
#   print "prop : ", prop
    print "The entropy of ", file_name, "is ", H
    

#   count.clear()
#   prop.clear()        
#   e = 2.71828
#   print math.log(e)
#   print math.log(8, 2)
#   print "hello"

# calc_entropy()

def calc():
    file_name = raw_input("Please input the file name: ")
    calc_entropy(file_name)
    p_count = count.copy()
    p_prop = prop.copy()
#   print "p_count : ", p_count
#   print "p_prop : ", p_prop
    count.clear()
    prop.clear()

    file_name = raw_input("Please input another file name: ")
    calc_entropy(file_name)
    q_count = count.copy()
    q_prop = prop.copy()
#   print "q_count : ", q_count
#   print "q_prop : ", q_prop
    count.clear()
    prop.clear()

    D = 0
    p_keys = p_count.keys() 
    for c in p_keys:
        if q_count.has_key(c):
            d = p_prop[c] * math.log((p_prop[c] / q_prop[c]), 2)
            D += d

    print "D(P||Q) : ", D


if __name__ == "__main__":
    calc()
```

程序运行结果：
![](/images/entropy.jpg)
