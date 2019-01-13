---
title: SSH Failed to Connect to CentOS7 in Vultr
date: 2018-11-06 11:15:46
categories:
tags:
---
SSH无法连接CentOS7(vultr)
现象一：
浏览器中无限循环输入用户名和密码，无法登陆console ![](ssh1.png) 
现象二：
SSH本地无法连接 ![](ssh2.png)
SSH跳板机也无法连接
![](ssh3.png) ![](ssh4.jpg) 
其他现象：
用Chrome打开Console，Ctrl+Alt+Del不起作用
Server disconnected (code: 1006) ![](ssh5.png)
检测发现没被墙。国内外可ping通, 22端口也是开启的。国内Tcping也是通的。小鸡上的服务也是可以正常使用的。
解决方案：
更换浏览器，用Microsoft Edge可以进入控制台
Send CtrlAltDel ![](ssh6.png)
按e编辑
![](ssh7.png)
 ro : readonly 只读
 rw : read write 即可以读，也可以写；接下来要更改配置文件，所以要写入
 init=/bin/bash 再次启动时进入/bin/bash 
![](ssh8.png)
Ctrl-X进入Bash
更改selinux配置
![](ssh9.png) ![](ssh10.png) ![](ssh11.png)
保存重启，可登陆console ![](ssh12.png)
SSH可连接 ![](ssh13.png)
折腾了一圈，Chrome现在Send CtrlAltDel也生效了。
困惑：
从来没用过selinux 。之前登陆,直接用passwd修改过root密码，可是一直能登陆的。

<逗比根据地>群里大佬的建议
touch /.autorelabel ![](ssh14.png)
原因：
可能是Vultr官方把selinux设置改了。因为之前ssh是可以连接的。
