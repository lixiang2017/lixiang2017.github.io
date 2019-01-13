---
title: Similar Strings
date: 2018-12-01 19:49:24
categories:
tags:
---
![](similar_strings.png)
```python
# Cloudin 云英 面试题
def is_similar(A, B):
    dict_a = {}
    dict_b = {}
    for i in A:
        if i in dict_a:
            dict_a[i] += 1
        else:
            dict_a[i] = 1
    for j in B:
        if j in dict_b:
            dict_b[j] += 1
        else:
            dict_b[j] = 1

    if dict_a == dict_b:
        return True
    else:
        return False


if __name__ == "__main__":
    A = "aac"
    B = "caa"
    print(is_similar(A, B))
    A = "aac"
    B = "caab"
    print(is_similar(A, B))
```
```python
# Cloudin 云英 面试题
from collections import Counter


def is_similar_collections(A, B):
    cnt_a = Counter(A)
    cnt_b = Counter(B)
    if cnt_a == cnt_b:
        return True
    else:
        return False


if __name__ == "__main__":
    A = "aac"
    B = "caa"
    print(is_similar_collections(A, B))
    A = "aac"
    B = "caab"
    print(is_similar_collections(A, B))
```
