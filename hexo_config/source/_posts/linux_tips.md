---
title: Linux Tips
date: 2018-07-24
categories: linux
tags:
---

# 替换某文件夹下所有文件中的字符串  

```bash
grep "John Doe" -rl  ./ | xargs sed -i "s/John Doe/lixiang/g"
```





