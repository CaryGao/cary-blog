---
title: '[原]org.zkoss.zk.ui.UiException: java.lang.NoSuchMethodException:'
tags: []
date: 2009-08-19 16:30:00
---

异常日志:

<textarea cols="90" rows="15" name="code" class="java:showcolumns">2009-8-19 16:29:48 org.zkoss.zk.ui.impl.UiEngineImpl handleError:1108
严重: &gt;&gt;org.zkoss.zk.ui.UiException: java.lang.NoSuchMethodException: class mo.org.sgvd.ui.domain.TfactSearch: name=course args=[class java.lang.String]
&gt;&gt;java.lang.NoSuchMethodException: class mo.org.sgvd.ui.domain.TfactSearch: name=course args=[class java.lang.String]
&gt;&gt;	at org.zkoss.lang.Classes.myGetAcsObj(Classes.java:954)
&gt;&gt;	at org.zkoss.lang.Classes.getAccessibleObject(Classes.java:882)
&gt;&gt;	at org.zkoss.lang.reflect.Fields.set(Fields.java:138)
&gt;&gt;	at org.zkoss.zkplus.databind.DataBinder.setBeanAndRegisterBeanSameNodes(DataBinder.java:1010)
&gt;&gt;	at org.zkoss.zkplus.databind.Binding.saveAttributeValue(Binding.java:368)
&gt;&gt;	at org.zkoss.zkplus.databind.Binding.access$100(Binding.java:48)
&gt;&gt;...</textarea> 

异常原因分析:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 仍然是ZK的UI引擎捕捉到的异常,这是由于ZK调用反射机制,从UI类中调用名字为course,参数类型为String的方法而导致异常.这种错误经常由于误写或者参数类型没有搞对.例如这里的course是个long类型,而ZK的大部分组件绑定的值,如value等都默认是String类型的.

解决方案:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 在绑定的数据上写转换类,将String转换成Long即可.

            <div>
                作者：wherejaly 发表于2009/8/19 16:30:00 [原文链接](http://blog.csdn.net/wherejaly/article/details/4463510)
            </div>
            <div>
            阅读：1636 评论：0 [查看评论](http://blog.csdn.net/wherejaly/article/details/4463510#comments)
            </div>