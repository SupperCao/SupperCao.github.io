---
layout:     post
title:      SpringMVC的使用-基于注解和实例
subtitle:   SpringMVC的使用-基于注解和实例
date:       2018-09-10
author:     BY
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - SpringMVC
---


# SpringMVC的使用-基于注解和实例

基于注解的配置主要用到两个注解`Controller`和`RequestMapping`<br/>
首先在原配置当中需要添加一个配置  `<context:component-scan base-package="包名" > </context:component-scan>` <br/>
这个配置主要是扫描这个包下面的注解,否则的注解是没有作用的。

#### 测试代码:

- 可以使用返回`ModelAndView`对象来实现
- 可以使用返回`String`来实现
- 可以使用`Map`来实现
- 首先是要在类上面加上`@Controller`

```

@Controller
public class AnnotationHandler {


    @RequestMapping("/modelAndViewTest")
    public ModelAndView modelAndViewTest(){
        //装载模型数据和逻辑视图
        ModelAndView modelAndView = new ModelAndView();
        //添加模型数据
        modelAndView.addObject("name","kangkang");
        //添加逻辑视图,也就是jsp页面, 比如show.jsp
        modelAndView.setViewName("show");
        return modelAndView;
    }


    @RequestMapping("/ModelTest")
    public String ModelTest(Model model){
        model.addAttribute("name","jerry");
        return "show";
    }

    @RequestMapping("/ModelMap")
    public String ModelMap(Map<String,String> map){
        map.put("name","zmy");
        return  "show";
    }


```
##### 以上方法都是可以在`localhost:8080/modelAndViewTest`这几个页面显示数据的

<br/>
基于注解的实例<br/>
看完了基于注解的实例,来完成一个在页面上填写数据然后返回到`SpringMVC`的例子<br/>
#### 首先配置`web.xml`

```
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>

  <!--处理中文乱码-->
  <filter>
    <filter-name>encodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
      <param-name>encoding</param-name>
      <param-value>utf-8</param-value>
    </init-param>
    <init-param>
      <param-name>forceEncoding</param-name>
      <param-value>true</param-value>
    </init-param>
  </filter>

  <filter-mapping>
    <filter-name>encodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>


  <!--设置访问静态资源,否则.css里面的文件加载不出来-->
  <servlet-mapping>
    <servlet-name>default</servlet-name>
    <url-pattern>*.css</url-pattern>
  </servlet-mapping>
  
  <!--DispatcherServlet主要用作职责调度工作，本身主要用于控制流程-->
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


</web-app>



```


`springmvc.xml`配置

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/cache"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/cache http://www.springframework.org/schema/cache/spring-cache.xsd">


    <context:component-scan base-package="com.imooc.handler" > </context:component-scan>

    <!--配置一个handler-->
    <bean id="testHandler" class="com.imooc.handler.MyHandler">

    </bean>

    <!--配置视图解析器-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <!--配置前缀-->
        <property name="prefix" value="/"></property>
        <property name="suffix" value=".jsp"/>

    </bean>


</beans>

```


`add.jsp`页面

```
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>add</title>
    <link href="css/bootstrap.min.css" rel="stylesheet">
    <style type="text/css">
        body{
            overflow-x:hidden;
        }
    </style>
</head>
<body>
<form class="form-horizontal" role="form" action="/addGoods" method="post">
    <div class="form-group">
        <label class="col-sm-1 control-label">名称</label>
        <div class="col-sm-3">
            <input type="text" class="form-control" name="name" placeholder="请输入商品名称">
        </div>
    </div>
    <div class="form-group">
        <label class="col-sm-1 control-label">价格</label>
        <div class="col-sm-3">
            <input type="text" class="form-control" name="price" placeholder="请输入商品价格">
        </div>
    </div>
    <div class="form-group">
        <div class="col-sm-offset-1 col-sm-3">
            <button type="submit" class="btn btn-default">提交</button>
        </div>
    </div>
</form>
</body>
</html>

```


写个`entity`类`Goods.java`

```

public class Goods {
    private String name;
    private double price;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }
}

```

最后在写一个类在处理逻辑<br/>

```
@RequestMapping("/addGoods")
    public ModelAndView addGoods(Goods goods){
        System.out.println(goods.getName()+"---"+goods.getPrice());
        ModelAndView modelAndView = new ModelAndView();
        modelAndView.addObject("goods",goods);
        modelAndView.setViewName("show");
        return modelAndView;


    }

```




