---
layout: shell
title: Shell Script for DSM
date: 2019-12-01 13:39:00
tags:
---
## 起因
DS Video根据文件夹中的文件生成索引，方便页面展示。
文件名称需要类似`S06.E03.mp4`或`S06.03.mp4` 才能被解析出第几季（Season）第几集（Episode）。否则，一个文件夹中的一季，没有显示在一块。
而，实际文件中是`生活大爆炸.H265.1080P.SE06.03.mkv`这样的，需要把`E`去掉才行。
生活大爆炸有12季，每一季大概有24集；群晖的管理界面中rename手动一个个改太麻烦了，而且很慢。
## 可行性
群晖是基于Linux的，shell是支持的。
## file path in DSM
```bash
/volume3/TV-Series/生活大爆炸6-11季.1080P.H265.非凡科技/S06
```
## shell script
```bash
#! /bin/bash
for i in {1..24}
do
	# echo 0$i
	# echo 墨镜MM.SE06.0$1.mp4
	# mv 墨镜MM.SE06.0$i.mp4 墨镜MM.S06.0$i.mp4
	if [ $i -lt 10 ]
	then
		i=0$i
		echo $i
	fi
	echo before renaming: 生活大爆炸.H265.1080P.SE06.$i.mkv
	mv 生活大爆炸.H265.1080P.SE06.$i.mkv 生活大爆炸.H265.1080P.S06.$i.mkv
	echo after renaming: ' ' 生活大爆炸.H265.1080P.S06.$i.mkv
done
echo '== after rename =='
ls -al *.mkv
```
## 其他季需要替换一下，vim substitute
```bash
:1,$s/06/09/g
```
## 问题
用脚本rename之后，DS Video中不能像手动那样自动更新索引。需要手动删除改文件夹，再添加该文件夹，reindex。
