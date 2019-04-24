---
title: if-else in Python
date: 2019-04-24 20:05:53
categories:
tags:
---
# 求两个数的较大值
```Python
# 1.常规
if a > b:
    c = a
else:
    c = b
# 2.表达式
c = a if a > b else b
# 3.列表
c = [b, a][a > b]
# 4.源自某个黑客
c = (a > b and [a] or [b])[0]
# 改编版
c = (a > b and a or b)
# 利用and的特点，若and前位置为假则直接判断为假。
# 利用or的特点，若or前位置为真则判断为真。
```
