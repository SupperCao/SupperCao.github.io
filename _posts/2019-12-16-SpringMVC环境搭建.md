---
layout:     post
title:      SpringMVC环境搭建
subtitle:   iOS定时器详解
date:       2019-12-16
author:     Cj
header-img: img/post-bg-ios9-web.jpg
catalog: 	 true
tags:
    - java
    - springmvc
---


# SpringMVC环境搭建

    
### 1. 引入依赖文件
```
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>4.3.1.RELEASE</version>
    </dependency>

    <!--导入servlet相关jar-->
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>3.1.0</version>
    </dependency>

```

### 2.SpringMVC.xml文件配置
下文已经配置好了`注解扫描配置`、`视图解析器`配置。

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

    <!--将AnnotationHandler自动扫描到IOC容器中-->
    <context:component-scan base-package="com.imooc.handler"></context:component-scan>


    <!--配置视图解析器-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <!--配置前缀-->
        <property name="prefix" value="/"></property>
        <!--配置前缀-->
        <property name="suffix" value=".jsp" ></property>

    </bean>

</beans>
```




### 3. 配置`web.xml`

直接复制到`web.xml`即可 <br/>
配置中包括了`中文乱码处理`，`css文件无法加载处理`, 还有配置`SpringMVC.xml`文件的配置

```
<web-app>
  <display-name>Archetype Created Web Application</display-name>
  <!--处理中文乱码-->
  <filter>
    <filter-name>encodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
      <param-name>encoding</param-name>
      <param-value>UTF-8</param-value>
    </init-param>
    <init-param>
      <param-name>forceEncodingFilter</param-name>
      <param-value>true</param-value>
    </init-param>
  </filter>

  <filter-mapping>
    <filter-name>encodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>

  <!--设置访问静态资源-->
  <servlet-mapping>
    <servlet-name>default</servlet-name>
    <url-pattern>*.css</url-pattern>
  </servlet-mapping>

  <servlet>
    <servlet-name>springmvc</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <!--配置springmvc.xml的路径-->
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:springmvc.xml</param-value>
    </init-param>
  </servlet>

  <servlet-mapping>
    <servlet-name>springmvc</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
  
</web-app>

```



   