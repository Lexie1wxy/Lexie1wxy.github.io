---
title: mysqlBug
date: 2020-07-08 00:24:01
tags:
- bug
categories: 
- Bug
- mysql
typora-root-url: ../_posts
---

# 修改mysql数据库的编码格式

## bug描述

.  Cause: java.sql.SQLException: Incorrect string value: '\xE9\x84\xA2\xE5\xAF\x92' for column 'name...

后来查看了mysql数据库的编码格式发现不对于是有了下面的解决方案

## (1)：

进入mysql的安装目录，找到my-default.ini或者my.ini配置文件，你可以将my-default.ini修改成my.ini，影响不大的；

## (2)：

我的my.ini只有一个[mysqld]标签，其他均处于注释状态，我们在my.ini里面做两件事

​        在[mysqld]标签下添加：character-set-server=utf8

​        增加一个[client]标签，并且在[client]标签下添加：default-character-set=utf8

## (3)：

到任务列表中重启mysql服务；

## (4)：

进入dos界面，登录数据库，输入命令：show variables like "%char%"；如果dos界面出现的下图所示结果，说明你修改mysql编码成功啦！

![image-20200708002604436](../images/mysqlBug/image-20200708002604436.png)



## (5)相关命令

`````java
net stop mysql
net start mysql
mysql -u root -p
show variables like 'char%';
`````

