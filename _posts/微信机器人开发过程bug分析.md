---
layout: post
title: 微信机器人开发过程bug分析
categories: [general，bug]
tags: [bug]
fullview: true
---

### bug-1

	警告: [SetContextPropertiesRule]{Context} Setting property 'source' to 'org.eclipse.jst.jee.server:CurrencyClientServe 


在Servers视图里双击创建的server，然后在其server的配置界面中选中"Publish module contexts to separate XML files"选项，之后把servers的项目删除 remove，再把tomcat服务器的配置文件修改，就是把你项目的配置删除，最后重新clean build ,这样就可以了。

### bug-2
	
	Allocate exception for servlet jsp

这种情况有两种可能

* jdk出错
  >此时，检查jdk版本，删除编译的文件夹，clean tomcat服务器和project，重新进行编译，如果错误仍然抛出，则说明不是jdk版本的问题。
  
* 导入的jar包出现问题
  >检查jar包引入的版本信息，删除多余无用的jar包，检查jar包冲突。

### bug-3

	java.lang.IllegalArgumentException: Document base E:\Eclipse\workspace\.metadata\.plugins\org.eclips 

错误原因：在eclipse中部署项目，eclipse找不到项目部署的临时文件，导致报错

解决办法：
（1）清除项目部署文件历史记录
（2）重新部署项目

### bug-4

	java.lang.ClassNotFoundException：（新建的servlet无法找到class文件）

重启eclipse，重新部署项目，用的是快捷方式中的tomcat，因为之前都是复制以前项目的代码，所以也会出现找不到路径的情况，新建一个servlet，eclipse会自动在web.xml中配置；所以如果是复制的代码，要记得web.xml中修改代码 

### 其他零碎收获

* 微信get只支持80端口
* 微信服务器必须要映射外网
* server一些默认配置比如访问地址，和项目部署地址会修改
* 导入的包要复制到WEB-INF/lib中
* 在项目中每个.java文件都没出错，但是工程上有个红叉，要么是jdk不统一，要么jar包missing
...