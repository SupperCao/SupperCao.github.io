---
layout:     post
title:      SpringMVC的使用-基于`xml`配置
subtitle:   SpringMVC学习关于xml配置
date:       2018-09-10
author:     BY
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - SpringMVC
---




# SpringMVC的使用-基于`xml`配置

基于SpringMVC我们只需要做:<br/>
1. `xml`配置`Controller`,`HandlerMapping`组件映射。<br/>
2. xml配置`ViewResolver(视图解析器)`组件映射。

#### 首先需要去`springmvc.xml`配置`HandlerMapping`:
```
配置HandlerMapping,将url请求映射到HandlerMapping
    <bean id="handlerMapping" class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping">
       <!--配置mapping-->
        <property name="mappings">
            <props>
                <!--配置test请求对应的handler-->
                <prop key="/test">testHandler</prop>
            </props>
        </property>

    </bean>
    
    <!--配置一个handler-->
    <bean id="testHandler" class="com.imooc.handler.MyHandler">

    </bean>
    
    
    <!--配置视图解析器-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <!--配置前缀-->
        <property name="prefix" value="/"></property>
        <property name="suffix" value=".jsp"/>

    </bean>

```


#### 配置`web.xml:`
```
<servlet>
    <servlet-name>SpringMVC</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:springmvc.xml</param-value>
    </init-param>
  </servlet>
  <servlet-mapping>
    <servlet-name>SpringMVC</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>

```



#### 写一个java测试类

```
public class MyHandler implements Controller {
    @Override
    public ModelAndView handleRequest(javax.servlet.http.HttpServletRequest request, javax.servlet.http.HttpServletResponse response) throws Exception {
        //装载模型数据和逻辑视图
        ModelAndView modelAndView = new ModelAndView();
        //添加模型数据
        modelAndView.addObject("name","Tom");
        //添加逻辑视图,也就是jsp页面, 比如show.jsp
        modelAndView.setViewName("show");
        return modelAndView;

    }

```

现在如果启动`tomcat`访问`/test`就会访问到`show.jsp`页面

<br/>

- `SimpleUrlHandlerMapping`是基于xml配置的Handler,如果是基于注解就不要使用这个否则会报错

- `InternalResourceViewResolver`配置视图解析器,目的是为了将`ModelAndView`返回的视图根据前缀后缀映射出来

