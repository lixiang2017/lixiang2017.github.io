---
title: Generate Verification Code in Python
date: 2018-12-16 19:20:10
categories:
tags:
---
```python
import random


def generate_verification_code(length=6):
    """随机生成6位的验证码"""
    code_list = []
    for i in range(10): # 0-9
        code_list.append(str(i))
    for i in range(ord("A"), ord("Z") + 1):
        code_list.append(chr(i))
    for i in range(ord("a"), ord("z") + 1):
        code_list.append(chr(i))

    veri_list = random.sample(code_list, length)
    return "".join(veri_list)


if __name__ == "__main__":
    print(generate_verification_code())
    print(generate_verification_code(8))
```
```cmd
ji0sYH
j8XfT9sh
```
###### REF
![](random.sample.png)
![](ord.png)
![](chr.png)
