---
title: 4 Ways of Fibonacci in Python
date: 2018-11-12 19:28:20
categories:
tags:
---
![](spiral.jpg)
```python
import numpy
import time

class Solution:
    '''1.递归法'''
    def fib_recur(self, n):
        assert n >= 0, "n >= 0"
        if n in (0, 1):
            return n
        return self.fib_recur(n - 1) + self.fib_recur(n - 2)

    '''2.memorization'''
    memo = {0: 0, 1: 1}
    def fib_recur_memo(self, n):
        if not n in Solution.memo:
            Solution.memo[n] = self.fib_recur_memo(n-1) + self.fib_recur_memo(n-2)
        return Solution.memo[n]

    '''3.递推法'''
    def fib_loop(self, n):
        a, b = 0, 1
        for i in range(n):
            a, b = b, a + b
        return a

    '''4.yield'''
    def fib_yield(self, n):
        a, b = 0, 1
        for i in range(n):
            a, b = b, a + b
        yield a

    '''5.矩阵法'''  # numpy
    def fib_matr(self, n):
        res = (numpy.matrix([[1, 1], [1, 0]]) ** (n - 1) * numpy.matrix([[1], [0]]))
        return res[0, 0]

    '''6.矩阵法''' # pow
    def fib_matr_pow(self, n):
        res = pow(numpy.matrix([[1, 1], [1, 0]]), n - 1) * numpy.matrix([[1], [0]])
        return res[0, 0]

'''7.类实现内部魔法方法'''
class Fibonacci(object):
    def __init__(self, num):
        self.num = num

    def __iter__(self):
        if self.num < 1:
            return 1
        a, b = 0, 1
        while self.num > 0:
            a, b = a + b, a
            self.num -= 1
        yield a

    def __next__(self):
        return self.__iter__()

if __name__ == "__main__":
    n = 45
    t1 = time.clock()
    print(Solution().fib_recur(n))
    t2 = time.clock()
    print("recursion time : ", t2 -t1)

    t1 = time.clock()
    print(Solution().fib_recur_memo(n))
    t2 = time.clock()
    print("recursion memo time : ", t2 - t1)

    t1 = time.clock()
    print(Solution().fib_loop(n))
    t2 = time.clock()
    print("loop time : ", t2 - t1)

    t1 = time.clock()
    print(Solution().fib_yield(n).__next__())
    t2 = time.clock()
    print("yield time : ", t2 - t1)

    t1 = time.clock()
    print(Solution().fib_matr(n))
    t2 = time.clock()
    print("matrix time : ", t2 - t1)

    t1 = time.clock()
    print(Solution().fib_matr_pow(n))
    t2 = time.clock()
    print("matrix (pow) time : ", t2 - t1)

    t1 = time.clock()
    print(Fibonacci(n).__iter__().__next__())
    t2 = time.clock()
    print("class time : ", t2 - t1)
```
![](fibonacci_time_2.png)
