---
title: 'ORA-01882: timezone region'
date: 2016-03-03 16:47:02
categories:
- java
tags: 
- oracle 
- java 
- weblogic
---

## 错误日志：
```
ORA-01882: timezone region
```
用weblogic配置连接池连到oracle时报错

<!-- more -->

## 错误原因：
原因是timezone没有设置

## 解决方法：
在jvm（Edit setDomainEnv.cmd）的参数后加入
```
-Duser.timezone=HKT
```

