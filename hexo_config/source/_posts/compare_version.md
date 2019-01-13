---
title: Compare Software Version
tags: [python, oj]
comments: true
categories: oj
---
# 比较任意两个软件版本号大小
请用您熟悉的编程语言，编程实现一个比较任意两个软件版本号大小的函数，如 1.2.3a 和 1.2.4b比较，后者版本号更大，请考虑各种情况，不可以使用系统提供的比较函数。   

```python
#! /usr/bin/python
import re

# a : 110a
# b : 120c
# great than : 1; equal : 0; less than : -1
def split_compare(a, b):
    l1 = len(a)
    l2 = len(b)
    a_former = '' 
    a_latter = ''
    b_former = ''
    b_latter = ''
    a_exist_alpha = 0
    b_exist_alpha = 0
    for i in range(l1):
        if a[i].isalpha():
            a_exist_alpha = 1
            a_former = a[:i]
            a_latter = a[i:]
            break
    if not a_exist_alpha:
        a_former = a

    for j in range(l2):
        if b[j].isalpha():
            b_exist_alpha = 1
            b_former = b[:j]
            b_latter = b[j:]
            break
    if not b_exist_alpha:
        b_former = b
    
#    print type(a_former), type(a_latter), type(b_former), type(b_latter)
#    print repr(a_former)
#    print a_former, a_latter, b_former, b_latter		

#    a_former = int(''.join([str(t) for t in a_former]))
#    b_former = int(''.join([str(t) for t in b_former]))

    if int(a_former) > int(b_former):
        return 1
    elif int(a_former) < int(b_former):
        return -1
    elif str(a_latter) > str(b_latter):
        return 1
    elif str(a_latter) < str(b_latter):
        return -1
    else:
        return 0

def version_compare(v1, v2):
    d1=re.split('\.', v1)
    d2=re.split('\.',v2)

#    d1=[int(d1[i]) for i in range(len(d1))]
#    d2=[int(d2[i]) for i in range(len(d2))]

    l = 0
    if len(d1) > len(d2):
        l = len(d1)
    else:
        l = len(d2)

    for i in range(l):
        try:
            if len(d1[i]) > 0 and len(d2[i]) > 0:
                if 1 == split_compare(d1[i], d2[i]):      
                    return '>'
                elif 0 == split_compare(d1[i], d2[i]):    
                    continue
                else:
                    return '<'
        except IndexError as e:
            if len(d1) > len(d2):
                return '>'
            else:
                return '<'
    return '='


if __name__=="__main__":
#    version1='2.6.9'
#    version2='12.0.9.2'
    version1 = raw_input("please input version1 :")
    version2 = raw_input("please input version2 :")
    print (version1, version_compare(version1, version2), version2)

#    a = raw_input("input a :")
#    b = raw_input("input b :")
#    print split_compare(a, b)
```
