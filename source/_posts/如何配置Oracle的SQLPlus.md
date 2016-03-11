---
title: 如何配置Oracle的SQLPlus
date: 2016-03-11 16:00:25
categories:
- Oracle
tags:
- oracle
- sqlplus
---

###SQL*Plus Overview
SQL*Plus是一个用于与Oracle Database交互和执行查询的工具，我们要安装的是命令行工具。
<!--more -->
###安装环境

 - Windows7 64位
 - Oracle 11g


###下载命令行工具
[点击这里进入官网下载](http://www.oracle.com/technetwork/topics/winx64soft-089540.html)，下载其中两个文件
```
instantclient-basic-windows.x64-12.1.0.2.0.zip
instantclient-sqlplus-windows.x64-12.1.0.2.0.zip
```
*其中basic是所有工具依赖的基本库，sqlplus是其中的命令行工具。*
###安装命令行工具
SQL*Plus命令行工具无需执行exe安装，所以只需将下载回来的两个文件解压到同一个目录即可，解压后文件名应该为`instantclient_12_1`，在运行工具之前我们需要在windows中配置以下环境变量，先右键计算机->属性->高级系统设置->环境变量,在系统变量中找到`Path`并在后面加上刚才解压后`instantclient_12_1`的目录与sdk子目录
```
C:\Program Files\instantclient_12_1\;C:\Program Files\instantclient_12_1\sdk;
```
再新增两个变量到系统环境中
```
TNS_ADMIN=C:\Program Files\instantclient_11_2
NLS_LANG=AMERICAN_AMERICA.UTF8
```
###测试连接数据库
打开CMD命令,输入以下
```
sqlplus 用户名/密码@数据库主机Ip
```
如果成功则CMD会显示`SQL>_`
###连接数据库详细语法
```
sqlplus username/password  
#如：普通用户登录  
sqlplus scott/tiger

sqlplus username/password@net_service_name 
#如: 
sqlplus scott/tiger@orcl

sqlplus  username/password as sysdba 
#如：
sqlplus sys/admin as sysdba
sqlplus username/password@//host:port/sid 
```
*注意：sys和system需要以sysdba登录*
###连接可能遇到的错误
笔者在用sqlplus连接时曾遇到以下报错
```
ORA-12514 TNS:listener does not currently know of service requested in connect descriptor
```
原因为环境变量中没有配置`TNS_ADMIN`，加上配置后错误就解决了。