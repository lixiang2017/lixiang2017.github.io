---
title: Tank
date: 2018-07-31 15:45:27
categories: oj
tags: [oj, python]
---
某次战役中，为便于信息交互，我军侦察部门将此次战役的关键高地坐标设定为（x=0，y=0）并规定，每向东增加100米，x加1，每向北增加100米，y加1。同时，我军情报部门也破译了敌军向坦克发送的指挥信号，其中有三种信号（L,R,M）用于控制坦克的运动，L 和 R 分别表示使令坦克向左、向右转向，M 表示令坦克直线开进100米，其它信号如 T 用于时间同步，P 用于位置较准。 一日，我军侦察兵发现了敌军的一辆坦克，侦察兵立即将坦克所在坐标（P, Q）及坦克前进方向（W：西，E：东，N：北，S：南）发送给指挥部，同时启动信号接收器，将坦克接收到的信号实时同步发往指挥部，指挥部根据这些信息得以实时掌控了该坦克的位置，并使用榴弹炮精准地击毁了该坦克。   请设计合理的数据结构和算法，根据坦克接收到的信号，推断出坦克所在的位置。 设计时请考虑可能的扩展情况，并体现出您的设计风格。 编码时请注重代码规范，并编写足够的单元测试。   假设，坦克坐标为（11，39）运行方向为 W，当收到以下信号 “MTMPRPMTMLMRPRMTPLMMTLMRRMP” 后，其位置应该为（9，43），运行方向为 E。

```python
#! /usr/bin/env python

turn_dict = {"EL" : "N", "WL" : "S", "SL" : "E", "NL" : "W", "ER" : "S", "WR" : "N", "SR" : "W", "NR" : "E"}

def action(now, command):
#   print "now : ", now, "command : ", command
#   print type(now)
    now = now.split()
#   print now
    
    # x, y, direction
    x = int(now[0])
    y = int(now[1])
    d = now[2]
#   print "x : ", x, ",y : ", y, ",d : ", d

    if "T" == command or "P" == command:
        pass
    elif "L" == command or "R" == command:
        turn_key = d + command
        d = turn_dict[turn_key]
    elif "M" == command:
        if "E" == d:
            x = x + 1
        elif "W" == d:
            x = x - 1
        elif "S" == d:
            y = y - 1
        elif "N" == d:
            y = y + 1
        else:
            pass
    else:
        pass

    now[0] = str(x)
    now[1] = str(y)
    now[2] = d

    next = " ".join(now)
    return next


if __name__ == "__main__":
    now = raw_input("please enter current location and direction of motion(e.g. x y w) : ")
    print "now : ", now
    command_list = raw_input("please enter the command list : ")
#   print "command_list : ", command_list

    for command in command_list:
        now = action(now, command)

    print "now : ", now 
```
