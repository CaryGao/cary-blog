---
title: 'Oracle - ORA-01840: input value not long enough for date format'
date: 2016-03-08 15:20:33
categories:
- oracle
tags:
- oracle
- java
---

## 错误日志：
```
Oracle - ORA-01840: input value not long enough for date format
```
在程式执行查询方法时，日志中出现以上错误

<!-- more -->

## 错误原因：
原因是查询语句中某个日期参数格式有问题，例如设置了`date = to_date('2015-02-29 08:53', 'yyyy-mm-dd hh24:mi:ss') `,而2015年根本没有2月29日，故而报错。

## 解决方法：
debug查找所有日期参数，看看格式是否正确。
