---
title: how-to-use-termtunnel
date: 2022-07-24 20:55:42
categories:
tags:
---


1. ### 简介
Termtunnel 是一个工具，它允许您通过多个跃点创建隧道或以非常简单的方式对抗内网隔离。与 lrzsz 一样，termtunnel 不仅支持文件传输，还支持网络代理。

翻译一下就是：
不管网络中间有多少跳，可以直接连接两端。
- 传文件，使用 upload/download 就可以。
- 网络代理支持服务器使用本地网络（remote_listen），也支持本地使用服务器网络（local_listen）。
这样服务器上访问外网，安装 rpm 等一些操作都可以通过代理；
同样，本地也可以直接打开内网 web 或连通内网数据库。

2. ### 网络拓扑 
使用mac连接远程服务器   
your_mac --- server1 --- server2 --- ... --- server_x --- your_target_server

3. ### 安装
两端都要安装 termtunnel, 中间的 server1/server2/.../server_x 不需要。
- mac上安装
```bash
# on mac
## a. brew 安装
brew install beordle/tap/termtunnel
## 或许需要sudo 
sudo brew install beordle/tap/termtunnel
# 或许需要公司的代理 or 梯子
http_proxy=http://192.168.50.12:3128  brew install beordle/tap/termtunnel
# b. 源码安装
# 如果你的系统版本过低，也可以采用源码编译安装。源码安装要先有这几个东西
brew install cmake make gcc
# 解压termtunnel.zip，进入目录里
cmake .
make

### 可能的异常，本地的protobuf可能版本太高，需要降级
sudo pip3 install protobuf==3.20.0
```

-  服务器端安装<br>
    - https://github.com/beordle/termtunnel/releases/tag/version-1.7.2
    - CentOS 7 使用 termtunnel-1.7.2-linux-amd64.tar.gz 解压放到 /usr/bin 这样PATH包含的路径下。


4. ### 使用方式 
- mac端  
假设只是一跳就直接到你的目标机器。如果是多跳，请看最后。
```bash
## mac端，只是在普通的ssh命令前加上 termtunnel
termtunnel ssh user_name@you_target_server -p server_port
# example
termtunnel ssh ysyd_xingzhiqian@192.168.100.40 -p 11442
```

- 服务器端（on your target server）  
把服务器上能连通的 10.170.207.137 40046 转发到本地 127.0.0.1 40042，
本地就可以通过 127.0.0.1 40042 连接了（数据库/web/...）
```bash
[root@host-10-170-207-138 ~]# termtunnel -a
termtunnel>
termtunnel>
termtunnel> help
List of command

  Command: local_listen
    port forward bind on local host

  Command: remote_listen
    port forward bind on remote host

  Command: upload
    upload a file

  Command: rz
    alias upload

  Command: download
    download a file

  Command: sz
    alias download

  Command: help
    view help manpage

  Command: exit
    exit application

termtunnel> local_listen 127.0.0.1 40042 10.170.207.137 40046
bind local port done
```
注意，如果想让别的机器访问这个 40042 端口，则需要把 127.0.0.1 改成 your_mac_ip。
因为 127.0.0.1 只会对本地监听，而非本地网段的网络。

5. ### 多跳
如果需要多跳。只需要两头使用 termtunnel，中间正常 ssh 即可。
```bash
## from your mac to server1
termtunnel ssh user_name1@server1 -p server1_port
## from server1 to server2
ssh user_name2@server2 -p server2_port
## from server2 to server3
ssh user_name3@server3 -p server3_port
...
## from server_x to your_target_server
ssh user_name_t@your_target_server  -p server_t_port
## on your target server 
termtunnel -a 
```


6. ### 想想为啥呢？
因为 termtunnel 封装了一层，中间的每次 shell 都还是在这次的连接会话里。
当然最后的 `termtunnel -a`，也是在这次连接里。
所以，多人同时用这种方式登录，不会冲突。各自会在自己的连接中。

7. ### 目前使用体验
- Termtunnel 传文件还算稳定，就是目前没有进度显示。可以解决 lrzsz 乱码失败的问题。
数据未传输完，直接 exit 会被警告。
- 堡垒机过期退出，会导致连接断开。需要重连。

8. #### ref
- https://www.v2ex.com/t/850426
- https://github.com/beordle/termtunnel

