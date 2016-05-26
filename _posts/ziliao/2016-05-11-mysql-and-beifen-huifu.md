---
layout: post
title: Linux下通过mysql自带命令备份恢复
category: 笔记
tags: MySQL
description: 在使用mysql的时候发现数据需要经常备份，所以在这写了这个备份恢复的文章。
---

mysqldump命令实现

## 1.备份（导出）

mysqldump -u 用户名 -p 数据库名 > 数据库名.sql（导出到当前目录下）

实例：

	mysqldump -u root -p mysqldb > mysqldb.sql
	
(将数据库mysqldb备份到mysqldb.sql中)

提示输入密码，此时输入正确的数据库登录密码即可

## 2.恢复（导入）

mysql -u 用户名 -p 数据库名 < 数据库名.sql（需要.sql文件在当前目录下）

需要先创建一个空数据库

　　mysql -u root -p(输入密码后进入mysql)

　　create database mysqldb;(创建一个名为mysqldb的数据库)

　　exit(退出mysql)

实例：

	mysql -u root -p mysqldb < mysqldb .sql
	
(从备份文件mysqldb .sql中导入数据到数据库mysqldb 中)

提示输入密码，此时输入正确的数据库登录密码即可
 

	
