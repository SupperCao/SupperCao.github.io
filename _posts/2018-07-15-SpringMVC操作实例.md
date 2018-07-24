---
layout:     post
title:      SpringMVC操作实例
subtitle:   
date:       2018-07-24
author:     CJ
header-img: img/home-bg-art.jpg
catalog: true
tags:
    - SpringMVC学习
---


# SpringMVC操作实例

---
## 使用注解开发

-  使用`@RequestMapping`注解: 完成URL映射的

首先把资源全部导入:这里是一个添加商品并显示的案例

1.把页面加载进来: add.jsp

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

2-   一个pojo类: goods

```
package com.imooc.handler.entity;

public class goods {
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

3- 创建一个Handler
 
```
    @RequestMapping("/addGoods")  //URL映射
    public ModelAndView addGoods(goods goods){
          System.out.println(goods.getName()+"----"+goods.getPrice());
          ModelAndView modelAndView = new ModelAndView();
          modelAndView.addObject("goods",goods); //在这里这个方法会直接映射到jsp页面也就是request域,所以jsp页面可以用el表达式请求到
          modelAndView.setViewName("show");  //设置返回的视图名称 也就是add.jsp页面跳转的页面,之所以不用写.jsp是因为springmvc里面已经配置好了
          return modelAndView;


    }


```

## 最后有两个问题
1. jsp页面的css可能加载不出来`解决方法`:在`web.xml`
文件中写入

```
<!--设置访问静态资源-->
    <servlet-mapping>
        <servlet-name>default</servlet-name>
        <url-pattern>*.css</url-pattern>
    </servlet-mapping>


```


2.  中文乱码问题: 也在`web.xml`文件中修改,添加一个filter

```
<filter>
        <filter-name>enCodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
        <init-param>
            <param-name>forceEncoding</param-name>
            <param-value>true</param-value>
        </init-param>
    </filter>

    <filter-mapping>
        <filter-name>enCodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

```
