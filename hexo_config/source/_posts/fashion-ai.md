---
title: FashionAI Data Preprocessing
date: 2018-07-25 16:48:06
categories:
tags:
---

# FashionAI全球挑战赛数据预处理

[活动官网1](http://fashionai.alibaba.com/)
[活动官网2](https://tianchi.aliyun.com/markets/tianchi/FashionAI)
[比赛官网](https://tianchi.aliyun.com/competition/introduction.htm?spm=5176.100066.0.0.13e433afjaR6SO&raceId=231649)

将10110张已经标注好的图片复制到对应文件夹中，方便后续的训练。
csv中对应数据如下：
Images/skirt_length_labels/73131f1c931056ee23ed8bf2a7910344.jpg	skirt_length_labels	nnnynn
Images/skirt_length_labels/969c50368b971adb5196f6c1f5f0b67c.jpg	skirt_length_labels	nynnnn

skirt_length一共有六种长度，对应六个文件夹。读取csv中某个图片对应的长度，将该图片复制到相应的文件中。暂时忽略模糊边界的情况。

```python
import os
import csv
import shutil

def copy_files(file_name, y_index):
    # print(file_name)
    # print(y_index)
    path = "D:\\tianchi\\python\\warm_up_train_20180201\\web\\Images\\skirt_length_labels"
    os.chdir(path)
    cwd = os.getcwd()
    # print(cwd)
    files = os.listdir()
    # print(files)

    dir0 = "D:\\tianchi\\python\\warm_up_train_20180201\\web\\classification\\None\\" + file_name
    dir1 = "D:\\tianchi\\python\\warm_up_train_20180201\\web\\classification\\SkirtLength0\\" + file_name
    dir2 = "D:\\tianchi\\python\\warm_up_train_20180201\\web\\classification\\SkirtLength1\\" + file_name
    dir3 = "D:\\tianchi\\python\\warm_up_train_20180201\\web\\classification\\SkirtLength2\\" + file_name
    dir4 = "D:\\tianchi\\python\\warm_up_train_20180201\\web\\classification\\SkirtLength3\\" + file_name
    dir5 = "D:\\tianchi\\python\\warm_up_train_20180201\\web\\classification\\SkirtLength4\\" + file_name

    if os.path.isfile(file_name):
        if y_index == 0:
            shutil.copyfile(file_name, dir0)
        elif y_index == 1:
            shutil.copyfile(file_name, dir1)
        elif y_index == 2:
            shutil.copyfile(file_name, dir2)
        elif y_index == 3:
            shutil.copyfile(file_name, dir3)
        elif y_index == 4:
            shutil.copyfile(file_name, dir4)
        elif y_index == 5:
            shutil.copyfile(file_name, dir5)

        # shutil.copyfile(file_name, "../../classification/")
    else:
        print("The file is not found")
    return

def classify():
    # cwd = os.getcwd()
    # print(cwd)

    os.chdir("D:\\tianchi\\python\\warm_up_train_20180201\\web\\Annotations")
    # path = os.getcwd()
    # print(path)

    # files = os.listdir()
    # print(files)
    csv_reader = csv.reader(open('skirt_length_labels.csv', encoding='utf-8'))
    for row in csv_reader:
        # print(row[0])
        # get the file name
        file_name = row[0].split('/')[2]
        # print(file_name)

        # get the index of yes
        # print(row[2])
        y_index = row[2].index('y')
        # print(y_index)

        # copy files
        copy_files(file_name, y_index)
    return

classify()
print("hello")
```

感谢[大佬](http://www.cjhang.com/)提示，代码可以改进一下：
1、15行路径可用变量简化一下：
```python
root = "D:\\tianchi\\python\\warm_up_train_20180201\\web\\classification\\"
```
2、65行return语句多余，python默认会return
