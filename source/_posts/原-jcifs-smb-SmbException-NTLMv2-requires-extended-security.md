---
title: '[原]jcifs.smb.SmbException: NTLMv2 requires extended security'
tags: []
date: 2009-09-23 15:30:00
---

錯誤日志:

<textarea cols="89" rows="9" name="code" class="java">jcifs.smb.SmbException: NTLMv2 requires extended security (jcifs.smb.client.useExtendedSecurity must be true if jcifs.smb.lmCompatibility &gt;= 3)
	jcifs.smb.NtlmPasswordAuthentication.getSigningKey(NtlmPasswordAuthentication.java:474)
	jcifs.smb.SmbSession.sessionSetup(SmbSession.java:295)
	jcifs.smb.SmbSession.send(SmbSession.java:234)
	jcifs.smb.SmbTree.treeConnect(SmbTree.java:161)
	jcifs.smb.SmbSession.logon(SmbSession.java:170)
	jcifs.smb.SmbSession.logon(SmbSession.java:163)
</textarea> 

錯誤原因:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 在使用NTLM与Spring Security时遇到上述问题,尚且不明白具体产生原因,初步估计是NTLM的Security与Spring Security有所冲突,参考资料发现做如下配置文件变动可解决问题.

<textarea cols="87" rows="10" name="code" class="java">		&lt;init-param&gt;
			&lt;param-name&gt;jcifs.smb.lmCompatibility&lt;/param-name&gt;
			&lt;param-value&gt;0&lt;/param-value&gt;
		&lt;/init-param&gt;
		&lt;init-param&gt;
			&lt;param-name&gt;
				jcifs.smb.client.useExtenededSecurity
			&lt;/param-name&gt;
			&lt;param-value&gt;false&lt;/param-value&gt;
		&lt;/init-param&gt;</textarea> 

&nbsp;

参考[http://lists.samba.org/archive/jcifs/2009-January/008356.html](http://lists.samba.org/archive/jcifs/2009-January/008356.html)

            <div>
                作者：wherejaly 发表于2009/9/23 15:30:00 [原文链接](http://blog.csdn.net/wherejaly/article/details/4584517)
            </div>
            <div>
            阅读：3859 评论：1 [查看评论](http://blog.csdn.net/wherejaly/article/details/4584517#comments)
            </div>