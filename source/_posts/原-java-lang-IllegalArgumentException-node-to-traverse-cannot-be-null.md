---
title: '[原]java.lang.IllegalArgumentException: node to traverse cannot be null!'
tags: []
date: 2009-09-12 09:56:00
---

錯誤日志:

<!-- more -->

<textarea cols="89" rows="15" name="code" class="java">严重: &gt;&gt;java.lang.IllegalArgumentException: node to traverse cannot be null!
&gt;&gt;	at org.hibernate.hql.ast.util.NodeTraverser.traverseDepthFirst(NodeTraverser.java:31)
&gt;&gt;	at org.hibernate.hql.ast.QueryTranslatorImpl.parse(QueryTranslatorImpl.java:254)
&gt;&gt;	at org.hibernate.hql.ast.QueryTranslatorImpl.doCompile(QueryTranslatorImpl.java:157)
&gt;&gt;	at org.hibernate.hql.ast.QueryTranslatorImpl.compile(QueryTranslatorImpl.java:111)
&gt;&gt;	at org.hibernate.engine.query.HQLQueryPlan.&lt;init&gt;(HQLQueryPlan.java:77)
&gt;&gt;	at org.hibernate.engine.query.HQLQueryPlan.&lt;init&gt;(HQLQueryPlan.java:56)
&gt;&gt;...</textarea> 

錯誤原因:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 通常此类错误都是由于HQL语句写的不正确,例如from写成了form,或者set A = 1 and B = 2,其中set不同字段用逗号","分离而不是用and.总之仔细检查HQL语句,看看有没有语法错误即可.

参考:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [http://geeklondon.com/blog/view/pesky-syntax](http://geeklondon.com/blog/view/pesky-syntax)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 

            <div>
                作者：wherejaly 发表于2009/9/12 9:56:00 [原文链接](http://blog.csdn.net/wherejaly/article/details/4545180)
            </div>
            <div>
            阅读：5930 评论：6 [查看评论](http://blog.csdn.net/wherejaly/article/details/4545180#comments)
            </div>