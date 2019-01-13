---
title: Chrome Aw Snap
date: 2018-11-12 12:04:16
categories:
tags:
---

帮我哥在win8上装了个Chrome,所有页面无法打开。重装Chrome也不行。提示"喔唷，崩溃啦！"

原因：百度残留的后台服务

解决办法：
 C:\Windows\System32\drivers\bd0001.sys
重命名bd0001.sys为bd0001.txt,重启删除该文件。

参考：
https://www.zhihu.com/question/29305453
