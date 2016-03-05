---
title: '[原]org.springframework.beans.factory.xml.XmlBeanDefinitionStoreException: Line 1 in XML document from class path resource'
tags: []
date: 2009-10-13 11:55:00
---

<textarea cols="50" rows="15" name="code" class="java">org.springframework.beans.factory.xml.XmlBeanDefinitionStoreException: Line 1 in XML document from class path resource [mo/com/sinokru/gxt/config] is invalid; nested exception is org.xml.sax.SAXParseException: Content is not allowed in prolog.
	at org.springframework.beans.factory.xml.XmlBeanDefinitionReader.doLoadBeanDefinitions(XmlBeanDefinitionReader.java:404)
	at org.springframework.beans.factory.xml.XmlBeanDefinitionReader.loadBeanDefinitions(XmlBeanDefinitionReader.java:342)
	at org.springframework.beans.factory.xml.XmlBeanDefinitionReader.loadBeanDefinitions(XmlBeanDefinitionReader.java:310)
	at org.springframework.beans.factory.support.AbstractBeanDefinitionReader.loadBeanDefinitions(AbstractBeanDefinitionReader.java:143)
	at org.springframework.beans.factory.support.AbstractBeanDefinitionReader.loadBeanDefinitions(AbstractBeanDefinitionReader.java:178)
	at org.springframework.beans.factory.support.AbstractBeanDefinitionReader.loadBeanDefinitions(AbstractBeanDefinitionReader.java:149)
	at org.springframework.web.context.support.XmlWebApplicationContext.loadBeanDefinitions(XmlWebApplicationContext.java:124)
	at org.springframework.web.context.support.XmlWebApplicationContext.loadBeanDefinitions(XmlWebApplicationContext.java:92)
	at org.springframework.context.support.AbstractRefreshableApplicationContext.refreshBeanFactory(AbstractRefreshableApplicationContext.java:123)
	at org.springframework.context.support.AbstractApplicationContext.obtainFreshBeanFactory(AbstractApplicationContext.java:423)
	at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:353)
	at org.springframework.web.context.ContextLoader.createWebApplicationContext(ContextLoader.java:255)
	at org.springframework.web.context.ContextLoader.initWebApplicationContext(ContextLoader.java:199)
	at org.springframework.web.context.ContextLoaderListener.contextInitialized(ContextLoaderListener.java:45)
	at org.mortbay.jetty.handler.ContextHandler.startContext(ContextHandler.java:530)
	at org.mortbay.jetty.servlet.Context.startContext(Context.java:135)
	at org.mortbay.jetty.webapp.WebAppContext.startContext(WebAppContext.java:1218)
	at org.mortbay.jetty.handler.ContextHandler.doStart(ContextHandler.java:500)
	at org.mortbay.jetty.webapp.WebAppContext.doStart(WebAppContext.java:448)
	at org.mortbay.component.AbstractLifeCycle.start(AbstractLifeCycle.java:40)
	at org.mortbay.jetty.handler.HandlerWrapper.doStart(HandlerWrapper.java:117)
	at org.mortbay.component.AbstractLifeCycle.start(AbstractLifeCycle.java:40)
	at org.mortbay.jetty.handler.HandlerWrapper.doStart(HandlerWrapper.java:117)
	at org.mortbay.jetty.Server.doStart(Server.java:217)
	at org.mortbay.component.AbstractLifeCycle.start(AbstractLifeCycle.java:40)
	at com.google.appengine.tools.development.JettyContainerService.startContainer(JettyContainerService.java:152)
	at com.google.appengine.tools.development.AbstractContainerService.startup(AbstractContainerService.java:116)
	at com.google.appengine.tools.development.DevAppServerImpl.start(DevAppServerImpl.java:218)
	at com.google.appengine.tools.development.gwt.AppEngineLauncher.start(AppEngineLauncher.java:86)
	at com.google.gwt.dev.HostedMode.doStartUpServer(HostedMode.java:365)
	at com.google.gwt.dev.HostedModeBase.startUp(HostedModeBase.java:589)
	at com.google.gwt.dev.HostedModeBase.run(HostedModeBase.java:397)
	at com.google.gwt.dev.HostedMode.main(HostedMode.java:232)</textarea>

            <div>
                作者：wherejaly 发表于2009/10/13 11:55:00 [原文链接](http://blog.csdn.net/wherejaly/article/details/4663162)
            </div>
            <div>
            阅读：1945 评论：0 [查看评论](http://blog.csdn.net/wherejaly/article/details/4663162#comments)
            </div>