---
title: '[原]org.zkoss.zk.ui.UiException: Out of bound:'
tags: []
date: 2009-08-19 15:42:00
---

异常日志:

<textarea cols="91" rows="15" name="code" class="java:showcolumns">2009-8-19 15:38:19 org.zkoss.zk.ui.impl.UiEngineImpl handleError:1108
严重: &gt;&gt;org.zkoss.zk.ui.UiException: Out of bound: 8 while size=7
&gt;&gt;	at org.zkoss.zul.Listbox.setSelectedIndex(Listbox.java:662)
&gt;&gt;	at sun.reflect.GeneratedMethodAccessor136.invoke(Unknown Source)
&gt;&gt;	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:25)
&gt;&gt;	at java.lang.reflect.Method.invoke(Method.java:585)
&gt;&gt;	at org.zkoss.lang.reflect.Fields.set(Fields.java:153)
&gt;&gt;	at org.zkoss.zkplus.databind.Binding.myLoadAttribute(Binding.java:316)
&gt;&gt;	at org.zkoss.zkplus.databind.Binding.loadAttribute(Binding.java:279)
&gt;&gt;	at org.zkoss.zkplus.databind.DataBinder$LoadOnSaveEventListener.loadAllBindings(DataBinder.java:1472)
&gt;&gt;...</textarea> 

异常原因分析:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ZK的UiException基本都出现在zul页面的元素错误,根据错误信息可以明显分析出是Listbox索引超出下标了.经过检查发现,两个Listbox同时绑定到一个数据上,而第一个Listbox组件拥有8个listitem,而第二个只有6个,当第一个listbox选中第7个时,就会发生索引越界.

解决方案:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 尽量不要多个组件绑定同一个数据.

            <div>
                作者：wherejaly 发表于2009/8/19 15:42:00 [原文链接](http://blog.csdn.net/wherejaly/article/details/4463254)
            </div>
            <div>
            阅读：2012 评论：0 [查看评论](http://blog.csdn.net/wherejaly/article/details/4463254#comments)
            </div>