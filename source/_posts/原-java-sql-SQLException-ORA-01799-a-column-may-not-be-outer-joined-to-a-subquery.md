---
title: '[原]java.sql.SQLException: ORA-01799: a column may not be outer-joined to a subquery'
tags: []
date: 2009-09-10 16:18:00
---

<textarea cols="86" rows="15" name="code" class="java">Caused by: java.sql.SQLException: ORA-01799: a column may not be outer-joined to a subquery

	at oracle.jdbc.driver.DatabaseError.throwSqlException(DatabaseError.java:111)
	at oracle.jdbc.driver.T4CTTIoer.processError(T4CTTIoer.java:330)
	at oracle.jdbc.driver.T4CTTIoer.processError(T4CTTIoer.java:287)
	at oracle.jdbc.driver.T4C8Oall.receive(T4C8Oall.java:742)
	at oracle.jdbc.driver.T4CPreparedStatement.doOall8(T4CPreparedStatement.java:215)
	at oracle.jdbc.driver.T4CPreparedStatement.executeForDescribe(T4CPreparedStatement.java:798)
	at oracle.jdbc.driver.OracleStatement.executeMaybeDescribe(OracleStatement.java:1038)
	at oracle.jdbc.driver.T4CPreparedStatement.executeMaybeDescribe(T4CPreparedStatement.java:838)
	at oracle.jdbc.driver.OracleStatement.doExecuteWithTimeout(OracleStatement.java:1131)
	at oracle.jdbc.driver.OraclePreparedStatement.executeInternal(OraclePreparedStatement.java:3284)
	at oracle.jdbc.driver.OraclePreparedStatement.executeQuery(OraclePreparedStatement.java:3328)
	at org.apache.commons.dbcp.DelegatingPreparedStatement.executeQuery(DelegatingPreparedStatement.java:93)
	at org.hibernate.jdbc.AbstractBatcher.getResultSet(AbstractBatcher.java:186)
	at org.hibernate.loader.Loader.getResultSet(Loader.java:1787)
	at org.hibernate.loader.Loader.doQuery(Loader.java:674)
	at org.hibernate.loader.Loader.doQueryAndInitializeNonLazyCollections(Loader.java:236)
	at org.hibernate.loader.Loader.doList(Loader.java:2213)
	... 32 more
</textarea>

错误原因:

&nbsp;&nbsp;&nbsp;&nbsp; Oracle禁止在outer join后使用子查询,参考[http://forums.oracle.com/forums/thread.jspa?threadID=945104&amp;tstart=0](http://forums.oracle.com/forums/thread.jspa?threadID=945104&amp;tstart=0)

Presumably, Oracle has decided that the 9i behavior was incorrect-- you are doing an outer join to a subquery, which isn't allowed. The 9.2.0.1 parser didn't notice the error. Presumably, you're getting lucky and Oracle generates the correct output. But presumably the optimizer doesn't know how to handle this properly in all cases, so Oracle disallows it. The 10.2.0.4 behavior appears to be correct from Oracle's standpoint-- you'll need to refactor the code to avoid doing an outer join to a subquery.

&nbsp;

翻译:据推测,Oracle 9i明白这种行为是错误的(你在outer join后使用子查询),但是9.2.0.1解析器没有提示这种错误,据推测,你非常幸运的生成了正确的输出.但是并不适用于所有情况.所以Oracle禁止这种操作.在10.2.0.4版本Oracle正确的拒绝这种操作,你应该重构你的代码来避免使用outer join后加入子查询.

&nbsp;

参考2 [http://www.oracle.com.cn/viewthread.php?tid=34336](Oracle安装/配置/入门)

ERROR at line 4:

ORA-01799: a column may not be outer-joined to a subquery
As a work around, you can use an inline view to achieve the desired effect: 

SELECT E.LNAME

FROM EMPLOYEE E,

(SELECT DEPT_ID FROM DEPARTMENT WHERE NAME = 'ACCOUNTING') V

WHERE E.DEPT_ID (+) = V.DEPT_ID;

&nbsp;

&nbsp;

&nbsp;

            <div>
                作者：wherejaly 发表于2009/9/10 16:18:00 [原文链接](http://blog.csdn.net/wherejaly/article/details/4539583)
            </div>
            <div>
            阅读：1937 评论：0 [查看评论](http://blog.csdn.net/wherejaly/article/details/4539583#comments)
            </div>