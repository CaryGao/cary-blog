---
title: '[原]java.lang.NullPointerException'
tags: []
date: 2009-08-19 16:39:00
---

异常日志:

<textarea cols="90" rows="15" name="code" class="java:showcolumns">严重: &gt;&gt;java.lang.NullPointerException
&gt;&gt;	at mo.org.sgvd.ui.convert.ConvertListboxToLong.coerceToUi(ConvertListboxToLong.java:33)
&gt;&gt;	at org.zkoss.zkplus.databind.Binding.myLoadAttribute(Binding.java:299)
&gt;&gt;	at org.zkoss.zkplus.databind.Binding.loadAttribute(Binding.java:279)
&gt;&gt;	at org.zkoss.zkplus.databind.DataBinder$LoadOnSaveEventListener.loadAllBindings(DataBinder.java:1472)
&gt;&gt;	at org.zkoss.zkplus.databind.DataBinder$LoadOnSaveEventListener.myLoadAllNodes(DataBinder.java:1375)
&gt;&gt;	at org.zkoss.zkplus.databind.DataBinder$LoadOnSaveEventListener.myLoadAllNodes(DataBinder.java:1384)
&gt;&gt;...</textarea> 

异常原因分析:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 这是笔者在工作中遇到最多的异常,其主要原因是因为一个为空的对象调用方法而导致的.例如:

<textarea cols="21" rows="2" name="code" class="java:showcolumns">Object obj = null;
obj.toString();</textarea> 

这个简单的例子中,obj为空对象,然后紧接着调用其toString();方法,就会导致以上异常.在日常工作中要十分注意此类问题,比如写了一些方法,某些参数如果为空,就会导致空指针异常,所以尽量在注释上标明此参数不能为空.或者加入为空判断,例如以上例子改写为:

<textarea cols="50" rows="6" name="code" class="java">Object obj = null;
if(obj != null) {
   obj.toString();
} else {
   //执行另外一些操作
}</textarea> 

            <div>
                作者：wherejaly 发表于2009/8/19 16:39:00 [原文链接](http://blog.csdn.net/wherejaly/article/details/4463557)
            </div>
            <div>
            阅读：642 评论：0 [查看评论](http://blog.csdn.net/wherejaly/article/details/4463557#comments)
            </div>