---
layout: post
title:  "Mysql 用户的创建和授权"
date:   2017-10-11 20:05:14 +0100
categories: mysql
author: tony
cover: "_assets/mysql.jpg"
location: Beijing, China
description: 新安装mysql后新建用户和对用户授权操作
---
---

## 登录MySQL
安装MySQL后，初始root没有密码。


```sql
mysql -h 127.0.0.1 -uroot
```

MySQL数据库的用户信息保存在mysql.user表中，可以使用sql语句查询结果。


```sql
use mysql;
select Host,User,Password from user;
```
查询到的结果如下： 

```
+------------------------------+------+
| Host                         | User |
+------------------------------+------+
| 127.0.0.1                    | root |
| ::1                          | root |
| localhost                    |      |
| localhost                    | root |
+------------------------------+------+
```
可以看到root用户只支持在本机登录。

## 创建用户
```sql  
insert into user(Host, User, Password) values("%", "user", password("1234"));
flush privileges;
```
Host为"%"标示可以从任何可以连接的机器登录。
再次查询用户表，可以看到现在结果如下：

```
+------------------------------+------+-------------------------------------------+
| Host                         | User | Password                                  |
+------------------------------+------+-------------------------------------------+
| localhost                    | root |                                           |
| 127.0.0.1                    | root |                                           |
| ::1                          | root |                                           |
| localhost                    |      |                                           |
| %                            | user | *A4B6157319038724E3560894F7F932C8886EBFCF |
+------------------------------+------+-------------------------------------------+
```
用户'user'的密码被加密后作为存储。
这时候，在其他的机器上可以使用user进行登录了。

## 权限授予
使用user用户登陆后，权限非常有限，需要使用命令授予user用户权限。
 
```sql
grant all privileges on *.* to 'user'@'%' identified by '1234' with grant option;
flush privileges;
```
如果不想开放所有的表，可以修改`*.*`为指定的表。

