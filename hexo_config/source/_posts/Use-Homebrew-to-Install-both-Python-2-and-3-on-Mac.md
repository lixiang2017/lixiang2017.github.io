---
title: Use-Homebrew-to-Install-both-Python-2-and-3-on-Mac
date: 2019-02-02 18:35:52
categories:
tags:
---
# 起因
公司项目使用Python2.7，自己LeetCode刷题想使用Python3

# 背景
macOS中自带了Python2.7，只需要安装Python3

# 安装Python3
一定要用 brew 安装 Python3 (不然很有可能会和系统的Python库有冲突)
```shell
$ brew install python3
```
上面的语句会自动安装 pip3
网上文章上都说用brew安装Python3会自带pip3的安装 
但是不知什么原因,我使用brew安装按成Python3后并没有pip3

# 安装pip3
## 下载文件
```shell
$ wget https://bootstrap.pypa.io/get-pip.py
$ python3 get-pip.py
```
## 创建软连接 到/usr/local/bin
```shell
$ ln -s /usr/local/Cellar/python/3.7.2_1/Frameworks/Python.framework/Versions/3.7/bin/pip3 /usr/local/bin/
$ which pip3
/usr/local/bin/pip3
$ cd /usr/local/Cellar/python/3.7.2_1/Frameworks/Python.framework/Versions/3.7/bin/
$ diff pip pip3
$
$ diff pip pip3.7
$
```
说明pip、pip3、pip3.7三个文件相同

# 安装virtualenv
```shell
$ sudo pip3 install virtualenv
```
![](sudo.jpg)
```shell
$ ln -s /usr/local/Cellar/python/3.7.2_1/Frameworks/Python.framework/Versions/3.7/bin/virtualenv /usr/local/bin
```
```shell
$ cd ~/lixiang2017_code/leetcode
$ virtualenv --no-site-packages venv_py3
```
![](wrong.jpg)
```shell
$ sudo virtualenv --no-site-packages venv_py3
```
![](wrong2.jpg)
# activate
![](activate.jpg)
# deactivate
![](deactivate.jpg)
