---
title: Transformer
date: 2018-12-01 22:24:58
categories:
tags:
---
![](transformer.jpg)
```python
# Cloudin 云英 面试题
def transformer(x, y):
    if x == y:
        return True
    elif x > y:
        return False
    elif x % 2 == 0:
        return transformer(x + 1, y) or transformer(2 * x, y)
    elif x % 2 == 1:
        return transformer(2 * x, y)


if __name__ == "__main__":
    x = 3
    y = 24
    assert transformer(x, y)
    x = 3
    y = 6
    assert transformer(x, y)
    x = 3
    y = 7
    assert transformer(x, y)
    x = 3
    y = 12
    assert transformer(x, y)
    x = 3
    y = 13
    assert transformer(x, y)
    x = 3
    y = 8
    assert not transformer(x, y)
    x = 3
    y = 9
    assert not transformer(x, y)
```
