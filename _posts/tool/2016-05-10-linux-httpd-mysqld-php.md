---
layout: post
title: Linux下安装搭建PHP运行环境
category: 工具
tags: [Linux 环境]
description: linux环境安装是学习linux必须要具备的技能之一
---

本文安装环境：CentOS 6.5

所需安装软件：

    Apache

    Mysql

    PHP

# 一、安装配置Apache服务

安装Apache

    yum install httpd -y
	
启动Apache

    /etc/init.d/httpd start
	
备注：Apache启动之后会提示如下错误：

    httpd:httpd: Could not reliably determine the server’s fully qualif domain name, using ::1 for ServerName

解决办法：

    vim /etc/httpd/conf/httpd.conf #编辑

找到 # ServerName www.example.com:80 # 

修改为 # ServerName www.suiblog.com:80 # 这里设置为你自己的域名，如果没有域名，可以设置为localhost

:wq! # 保存退出

设为开机启动

    chkconfig httpd on
	
重启Apache

    /etc/init.d/httpd restart

# 二丶安装配置Mysql服务

    yum install mysql mysql-server
	
询问是否要安装，输入Y即可自动安装,直到安装完成

这里可能出现依赖关系的错误提示，如：

    perl-DBD-MySQL is needed by mysql-server-5.1.73-3.el6_5.i686

可参照一下解决，之后再执行第一条命令

    yum install perl-DBD-MySQL
	
启动MySQL

    /etc/init.d/mysqld start
	
设为开机启动

    chkconfig mysqld on

拷贝配置文件（注意：如果/etc目录下面默认有一个my.cnf，直接覆盖即可）

    cp  -f /usr/share/mysql/my-medium.cnf  /etc/my.cnf
 
设置密码

    mysql_secure_installation
	
回车，根据提示输入Y

输入2次密码，回车

根据提示一路输入Y

最后出现：Thanks for using MySQL!

MySql密码设置完成，重新启动 MySQL

修改用户Host，支持远程访问数据库

    mysql -uroot -p123456
	
     mysql>  use mysql

     mysql>  select Host,User from user;

     mysql>  update user set Host=’%’ where User=’root’;   #出现错误提醒（正常）

     mysql>  flush privileges;

     mysql>  select Host,User from user;   # 再查看下效果

# 三丶安装PHP

    yum -y install php
 
安装PHP组件，使 PHP5 支持 MySQL

    yum -y install php-mysql php-gd php-imap php-ldap php-odbc php-pear php-xml php-xmlrpc

做最后的重启

重启MySql

    service mysqld restart
	
重启Apche

    service httpd restart