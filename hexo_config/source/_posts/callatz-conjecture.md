---
title: Callatz Conjecture(3n+1 Conjecture) in Matlab
date: 2018-11-26 10:08:27
categories:
tags:
---

```Matlab
% 考拉兹猜想（Collatz conjecture）/ 3n+1猜想
% 对所有自然数，如果它是奇数，则对它乘3再加1，如果它是偶数，则对它除以2，如此循环，最终都能够得到1。    
% matlab
while 1
    n = input('please input n :')
    if n <= 0  break
    end

    while n > 1
        if rem(n, 2) == 0
            n = n / 2
        else
            n = 3 * n + 1
        end
        fprintf('\n n = %d', n)
    end
end
```
