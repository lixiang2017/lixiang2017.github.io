---
title: System Path of Python in Windows and Ubuntu
date: 2018-11-30 17:40:47
categories:
tags:
---

```python
import sys

# print(sys.path)
print("\n".join(sys.path))
```
###### Windows(PyCharm)
```dos
C:\Users\lixiang\PycharmProjects\other
C:\Users\lixiang\PycharmProjects\other
C:\Users\lixiang\PycharmProjects\other\venv\Scripts\python36.zip
C:\Users\lixiang\AppData\Local\Programs\Python\Python36\DLLs
C:\Users\lixiang\AppData\Local\Programs\Python\Python36\lib
C:\Users\lixiang\AppData\Local\Programs\Python\Python36
C:\Users\lixiang\PycharmProjects\other\venv
C:\Users\lixiang\PycharmProjects\other\venv\lib\site-packages
C:\Users\lixiang\PycharmProjects\other\venv\lib\site-packages\setuptools-28.8.0-py3.6.egg
```
###### Windows(IPython)
```dos

C:\Users\lixiang\AppData\Local\Programs\Python\Python36\Scripts\ipython.exe
c:\users\lixiang\appdata\local\programs\python\python36\python36.zip
c:\users\lixiang\appdata\local\programs\python\python36\DLLs
c:\users\lixiang\appdata\local\programs\python\python36\lib
c:\users\lixiang\appdata\local\programs\python\python36
c:\users\lixiang\appdata\local\programs\python\python36\lib\site-packages
c:\users\lixiang\appdata\local\programs\python\python36\lib\site-packages\IPython\extensions
C:\Users\lixiang\.ipython
```

###### Python3.6 in Ubuntu
```bash

/usr/lib/python36.zip
/usr/lib/python3.6
/usr/lib/python3.6/lib-dynload
/usr/local/lib/python3.6/dist-packages
/usr/lib/python3/dist-packages
```
###### Python2.7 in Ubuntu
```bash

/usr/lib/python2.7
/usr/lib/python2.7/plat-x86_64-linux-gnu
/usr/lib/python2.7/lib-tk
/usr/lib/python2.7/lib-old
/usr/lib/python2.7/lib-dynload
/usr/local/lib/python2.7/dist-packages
/usr/lib/python2.7/dist-packages
```
