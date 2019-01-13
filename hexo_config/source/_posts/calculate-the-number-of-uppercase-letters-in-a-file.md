---
title: Calculate the Number of Uppercase Letters in a File
date: 2018-11-27 00:10:55
categories:
tags:
---

```python
import os
os.chdir("C:\\users\\lixiang\\desktop")

with open("file.txt") as file:
    count = 0
    for i in file.read():
        if i.isupper():
            count += 1
print(count)
```
