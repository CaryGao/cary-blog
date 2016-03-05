---
title: '[原]org.hibernate.QueryException: query specified join fetching, but the owner of the fetched association was not present in the sel'
tags: []
date: 2009-08-21 09:50:00
---

错误日志:

<textarea cols="91" rows="15" name="code" class="java:showcolumns">2009-8-20 12:17:56 org.zkoss.zk.ui.impl.UiEngineImpl handleError:1108
严重: &gt;&gt;java.lang.IllegalArgumentException: org.hibernate.QueryException: query specified join fetching, but the owner of the fetched association was not present in the select list [FromElement{explicit,not a collection join,fetch join,fetch non-lazy properties,classAlias=null,role=null,tableName=SGVD.TPROFILE,tableAlias=tprofile1_,origin=SGVD.TPROFILEPERSON tprofilepe0_,colums={tprofilepe0_.PROFILEID ,className=mo.org.sgvd.domain.Tprofile}}] [SELECT pfp.tprofile FROM mo.org.sgvd.domain.Tprofileperson pfp left join fetch pfp.tprofile WHERE pfp.tperson.personid = 114]
&gt;&gt;org.hibernate.QueryException: query specified join fetching, but the owner of the fetched association was not present in the select list [FromElement{explicit,not a collection join,fetch join,fetch non-lazy properties,classAlias=null,role=null,tableName=SGVD.TPROFILE,tableAlias=tprofile1_,origin=SGVD.TPROFILEPERSON tprofilepe0_,colums={tprofilepe0_.PROFILEID ,className=mo.org.sgvd.domain.Tprofile}}] [SELECT pfp.tprofile FROM mo.org.sgvd.domain.Tprofileperson pfp left join fetch pfp.tprofile WHERE pfp.tperson.personid = 114]
&gt;&gt;	at org.hibernate.hql.ast.tree.SelectClause.initializeExplicitSelectClause(SelectClause.java:195)
&gt;&gt;	at org.hibernate.hql.ast.HqlSqlWalker.useSelectClause(HqlSqlWalker.java:705)
&gt;&gt;	at org.hibernate.hql.ast.HqlSqlWalker.processQuery(HqlSqlWalker.java:529)
&gt;&gt;	at org.hibernate.hql.antlr.HqlSqlBaseWalker.query(HqlSqlBaseWalker.java:645)
&gt;&gt;	at org.hibernate.hql.antlr.HqlSqlBaseWalker.selectStatement(HqlSqlBaseWalker.java:281)
&gt;&gt;...</textarea> 

错误原因分析:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 首先看HQL语句:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; SELECT pfp.tprofile FROM Tprofileperson pfp left join fetch pfp.tprofile WHERE pfp.tperson.personid = 114

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 此处我希望加载Tprofileperson下的tprofile,而我使用了fetch来立即抓取tprofile,错误就在这里.如果你使用fetch,那么fetch左边的连接对象(拥有者)一定要出现在select后,例如将上面改为select pfp... 这样就会执行正常,因为使用了fetch,Hibernate就会将需要fetch的对象(Tprofile)立即加载在父对象(Tprofileperson)中,而我的select确只是列出子对象,而拥有者(Tprofileperson)并没有present(出席在结果集中),那么就会出现以上错误.

&nbsp;&nbsp;&nbsp;&nbsp; 下面我们看另外会出现同样错误的语句:

&nbsp;&nbsp;&nbsp;&nbsp; <textarea cols="50" rows="3" name="code" class="java">01: select person from Person as person
02: left join person.address as address
03: left join fetch address.country as country</textarea> 

你可以看到在第3行使用了fetch,而第2行确没有使用fetch,那么第3行fetch的拥有者address并没有立即被抓取,这就会导致同样的错误,将第2行中的join后加上fetch,即可解决问题.

总结:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 如果使用了fetch,那么拥有者一定要present,也就是对象一定要被加载出来

参考资料:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [http://lamnguyenblog.com/2008/10/common-hibernate-errors-and-causes/](http://lamnguyenblog.com/2008/10/common-hibernate-errors-and-causes/)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [http://www.google.com/custom?hl=en&amp;lr=&amp;ie=utf-8&amp;oe=utf-8&amp;client=pub-2698861478625135&amp;cof=FORID%3A1%3BGL%3A1%3BLBGC%3A336699%3BLC%3A%230000ff%3BVLC%3A%23663399%3BGFNT%3A%230000ff%3BGIMP%3A%230000ff%3BDIV%3A%23336699%3B&amp;q=org.hibernate.QueryException%3A+query+specified+join+fetching%2C+but+the+owner+of+the+fetched+association+was+not+present+in+the+select+list](http://www.google.com/custom?hl=en&amp;lr=&amp;ie=utf-8&amp;oe=utf-8&amp;client=pub-2698861478625135&amp;cof=FORID%3A1%3BGL%3A1%3BLBGC%3A336699%3BLC%3A%230000ff%3BVLC%3A%23663399%3BGFNT%3A%230000ff%3BGIMP%3A%230000ff%3BDIV%3A%23336699%3B&amp;q=org.hibernate.QueryException%3A+query+specified+join+fetching%2C+but+the+owner+of+the+fetched+association+was+not+present+in+the+select+list)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;

            <div>
                作者：wherejaly 发表于2009/8/21 9:50:00 [原文链接](http://blog.csdn.net/wherejaly/article/details/4468772)
            </div>
            <div>
            阅读：5100 评论：4 [查看评论](http://blog.csdn.net/wherejaly/article/details/4468772#comments)
            </div>