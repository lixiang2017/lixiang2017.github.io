---
title: List Files and Directory Tree Structure in Python
date: 2018-12-16 15:45:02
categories:
tags:
---
```python
import os


def walk(path):
    l = []
    file_dir_list = os.listdir(path)
    if not file_dir_list:
        return []
    for item in file_dir_list:
        if os.path.isfile(path + "\\" + item):
            l.append(item)
        else:
            l += walk(path + "\\" + item)

    return l


def dfs_show_dir(path, depth):
    if depth == 0:
        print("root: [" + path + "]")

    for item in os.listdir(path):
        print("|  " * depth + "+--" + item)

        new_item = path + "/" + item
        if os.path.isdir(new_item):
            dfs_show_dir(new_item, depth + 1)


if __name__ == "__main__":
    path = os.getcwd()
    os.chdir("C:\\Users\\lixiang\\PycharmProjects\\other\\testcase_for_walk")
    path = os.getcwd()
    print(walk(path), "\n")

    dfs_show_dir(path, 0)
```
![](dir_structure.png)
```cmd
['4.txt', '5.txt', '6.txt'] 

root: [C:\Users\lixiang\PycharmProjects\other\testcase_for_walk]
+--1
|  +--2
|  +--3
|  |  +--4.txt
|  |  +--5.txt
|  +--6.txt
```
