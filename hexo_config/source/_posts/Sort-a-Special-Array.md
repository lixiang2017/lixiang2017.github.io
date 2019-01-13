---
title: Sort a Special Array
date: 2018-12-02 00:36:16
categories:
tags:
---
![](sort.png)
```python
# Cloudin云英 面试题
def sort_special_array(a):
    if not a:
        return a

    ls = []
    i = 0
    j = len(a) - 1
    k = 0
    if a[0] < a[-1]:
        ls.append(a[0])
        i += 1
    else:
        ls.append(a[-1])
        j -= 1

    while i <= j:
        if ls[k] == a[i]:
            i += 1
            continue
        if ls[k] == a[j]:
            j -= 1
            continue
        if a[i] < a[j]:
            ls.append(a[i])
            i += 1
            k += 1
        else:
            ls.append(a[j])
            j -= 1
            k += 1

    return ls


if __name__ == "__main__":
    a = [-4, -2, -2, 0, 4, 5, 7, 8, 7, 5, 4, 3, 2, 0, 0, -3, -5]
    assert sort_special_array(a) == [-5, -4, -3, -2, 0, 2, 3, 4, 5, 7, 8]
    a = [-4, -2, -2, 0, 4, 5, 7]
    assert sort_special_array(a) == [-4, -2, 0, 4, 5, 7]
    a = [4, 2, 2]
    assert sort_special_array(a) == [2, 4]
    a = [5]
    assert sort_special_array(a) == [5]
    a = []
    assert sort_special_array(a) == []
```
