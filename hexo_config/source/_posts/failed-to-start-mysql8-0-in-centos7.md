---
title: Failed to Start Mysql8.0 in Centos7(vultr)
date: 2019-01-20 18:38:05
categories:
tags:
---
## 启动失败
![](75749952.png)
![](75771201.png)
## 查看日志
![](75840236.png)
原因：内存不足
![](vultr_hardinfo.jpg)
[Solution](https://blog.csdn.net/Mr_OOO/article/details/78653523)
![](76140575.png)
![](76232995.png)
## 成功开启MySQL
## 获取临时密码
```bash
grep "A temporary password" /var/log/mysqld.log  
# 修改root密码，必须包含大小写特殊字母
mysql -u root -p
alter user 'root'@'localhost' identified by 'your_password';
```
## 使用DBeaver客户端连接失败
![](71003550.png)
```cmd
Communications link failure
The last packet sent successfully to the server was 0 milliseconds ago. The driver has not received any packets from the server.
  Connection refused (Connection refused)
```
## Solution
### 远程测试端口是否开启
![](71918674.png)
### 服务器本机查看端口是否开启
![](71982775.png)
![](72127872.png)
原因：防火墙中端口没有开启
```bash
[root@vultr ~]# firewall-cmd --zone=public --list-ports
[root@vultr ~]# firewall-cmd --zone=public --list-ports | grep 3306
[root@vultr ~]# firewall-cmd --zone=public --add-port=3306/tcp --permanent
success
[root@vultr ~]# firewall-cmd --zone=public --add-port=3306/udp --permanent
success
[root@vultr ~]# firewall-cmd --zone=public --list-ports
[root@vultr ~]# firewall-cmd --reload
success
[root@vultr ~]# firewall-cmd --zone=public --list-ports
```
![](72326504.png)
```cmd
null, message from server: "Host '61.148.199.222' is not allowed to connect to this MySQL server"
```
## 服务器本地可以登录
![](35968830.png)
## 客户端无法登录，Public Key Retrieval is not allowed
![](36006075.png)
修改DBeaver中驱动属性，allowPublicKeyRetrieval属性值改为true
![](36115949.png)
## 连接成功
![](36201778.png)

