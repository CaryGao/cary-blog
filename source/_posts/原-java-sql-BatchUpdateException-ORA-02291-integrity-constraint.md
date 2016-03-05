---
title: '[原]java.sql.BatchUpdateException: ORA-02291: integrity constraint'
tags: []
date: 2009-08-31 12:07:00
---

錯誤日志:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <textarea cols="88" rows="15" name="code" class="java">[31 12:02:03,906 WARN ] [Thread-11] util.JDBCExceptionReporter - SQL Error: 2291, SQLState: 23000
2009-8-31 12:02:04 org.zkoss.zk.ui.impl.UiEngineImpl handleError:1108
严重: &gt;&gt;org.springframework.dao.DataIntegrityViolationException: Could not execute JDBC batch update; nested exception is org.hibernate.exception.ConstraintViolationException: Could not execute JDBC batch update
&gt;&gt;org.hibernate.exception.ConstraintViolationException: Could not execute JDBC batch update
[SQL: 2291, 23000]
&gt;&gt;java.sql.BatchUpdateException: ORA-02291: integrity constraint (SGVD.TFACTCANCELLI_FK61247830083984) violated - parent key not found
&gt;&gt;
&gt;&gt;	at oracle.jdbc.driver.DatabaseError.throwBatchUpdateException(DatabaseError.java:342)
&gt;&gt;	at oracle.jdbc.driver.OraclePreparedStatement.executeBatch(OraclePreparedStatement.java:10656)
&gt;&gt;	at org.apache.commons.dbcp.DelegatingStatement.executeBatch(DelegatingStatement.java:297)
&gt;&gt;	at org.hibernate.jdbc.BatchingBatcher.doExecuteBatch(BatchingBatcher.java:48)
&gt;&gt;	at org.hibernate.jdbc.AbstractBatcher.executeBatch(AbstractBatcher.java:246)
&gt;&gt;...</textarea> 

&nbsp;

錯誤分析:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 从字面来看,此错误为外键约束错误,经过检查发现,某字段在数据库中设置外键与Hibernate中引用的表对象不同而导致错误.

&nbsp;

            <div>
                作者：wherejaly 发表于2009/8/31 12:07:00 [原文链接](http://blog.csdn.net/wherejaly/article/details/4502696)
            </div>
            <div>
            阅读：4967 评论：1 [查看评论](http://blog.csdn.net/wherejaly/article/details/4502696#comments)
            </div>