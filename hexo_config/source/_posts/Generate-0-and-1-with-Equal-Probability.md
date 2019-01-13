---
title: Generate 0 and 1 with Equal Probability
date: 2018-11-12 23:00:55
categories:
tags:
---
一个有问题的解法：
![](infinite_loop.jpg)
上述解法在i,j取值为0,0和1,1时，均造成死循环。正确的做法应该是把原始随机函数放入while中。
```python
#小年糕面试题
# given     A()  return 0 1  probability: p 1-p
# implement B()  return 0 1  probability: 50% 50%

def B():
    while(True):
        i = A()
        j = A()
        if((0 == i) and (1 == j)):   # p*(1-p)
            return 0
        elif((1 == i) and (0 == j)): # (1-p)*p
            return 1
```


