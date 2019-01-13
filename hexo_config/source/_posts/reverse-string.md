---
title: Reverse String
date: 2018-10-24 00:19:01
categories:
tags: [python]
---
# Python实现字符串反转的四种方法
1. 切片

```python
def rev(s):
    return s[::-1]
```
这是采用切片的方法，设置步长为-1，也就是反过来排序。这种方法是最简洁的，也是最推荐的。

2. 传统方法
```python
def rev(s):
    str0 = ”
    l = len(s)-1
    while l >= 0:
        str0 += s[l]
        l -= 1
    return str0
```
这种方法是先设置一个str0的空变量，然后在s中从后往前取值，然后追加到str0中。

3.列表
```python
def rev(s):
    a = list(s)
    a.reverse()
    return ”.join(a)
```
这种方法是采用列表的reverse方法，先将s转换为列表，然后通过reverse方法反转，然后在通过join连接为字符串。

注意：这里注意区分列表的reverse和sort（或sorted）方法：
reverse是把列表方向排序;
sort(reverse=True)是按照某种顺序方向排序。
example:
>>> a=['a','c','b','d']
>>> b=['a','c','b','d']
>>> a.sort(reverse=True)
>>> b.reverse()
>>> a
['d', 'c', 'b', 'a']
>>> b
['d', 'b', 'c', 'a']

4. reduce
```python
from functools import reduce
def rev(s):
    return reduce(lambda x, y : y + x, s)
```
