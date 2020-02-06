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
# 比较两个文本文件。以前者作为参考，不一致的输出行号
```bash
# awk '{if(NR==FNR){arr[NR]=$0}else{if(arr[FNR]!=$0){print FNR}}}' test test1
3 
# cat test
a aa aaa 1
b bb bbb 2
c cc ccc
d dd ddd 4
e ee eee 5
# cat test1
a aa aaa 1
b bb bbb 2
c cc ccc 3
d dd ddd 4
e ee eee 5
```
# 解析
当读取第一个文件的时候NR和FNR都是从1开始计数，这时NR==FNR 将行全部内容赋值给数组arr。当读取到第二个文件时，NR!=FNR此时表示已读第二个文件，将arr的内容和$0进行比较如果不相同，则输出行号。

# awk
```bash
# echo "hello lixiang" | awk '{$2="parim,"; $3="how"; $4="are"; $5="you?"; print $0}'
hello parim, how are you?
```

