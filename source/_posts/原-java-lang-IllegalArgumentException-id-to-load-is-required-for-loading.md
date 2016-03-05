---
title: '[原]java.lang.IllegalArgumentException: id to load is required for loading'
tags: []
date: 2009-10-24 11:11:00
---

2009-10-24 10:58:57 org.zkoss.zk.ui.impl.UiEngineImpl handleError:1108

严重: &gt;&gt;java.lang.IllegalArgumentException: id to load is required for loading

<!-- more -->

&gt;&gt;&nbsp;&nbsp;&nbsp; at org.hibernate.event.LoadEvent.&lt;init&gt;(LoadEvent.java:51)

&gt;&gt;&nbsp;&nbsp;&nbsp; at org.hibernate.event.LoadEvent.&lt;init&gt;(LoadEvent.java:33)

&gt;&gt;&nbsp;&nbsp;&nbsp; at org.hibernate.impl.SessionImpl.get(SessionImpl.java:812)

&gt;&gt;&nbsp;&nbsp;&nbsp; at org.hibernate.impl.SessionImpl.get(SessionImpl.java:808)

&gt;&gt;&nbsp;&nbsp;&nbsp; at org.hibernate.ejb.AbstractEntityManagerImpl.find(AbstractEntityManagerImpl.java:182)

&gt;&gt;&nbsp;&nbsp;&nbsp; at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)

&gt;&gt;&nbsp;&nbsp;&nbsp; at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:39)

&gt;&gt;&nbsp;&nbsp;&nbsp; at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:25)

&gt;&gt;&nbsp;&nbsp;&nbsp; at java.lang.reflect.Method.invoke(Method.java:585)

&gt;&gt;&nbsp;&nbsp;&nbsp; at org.springframework.orm.jpa.ExtendedEntityManagerCreator$ExtendedEntityManagerInvocationHandler.invoke(ExtendedEntityManagerCreator.java:357)

&gt;&gt;...

&nbsp;

原因:使用JPA时，当使用find(Class&lt;T&gt; clazz, Serializable id);此方法時，若id為空，則會出現以上錯誤。

            <div>
                作者：wherejaly 发表于2009/10/24 11:11:00 [原文链接](http://blog.csdn.net/wherejaly/article/details/4722370)
            </div>
            <div>
            阅读：4209 评论：1 [查看评论](http://blog.csdn.net/wherejaly/article/details/4722370#comments)
            </div>