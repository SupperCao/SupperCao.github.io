---
layout:     post
title:      Mybatis中`mapper`代理方式报错
subtitle:   mapper代理方式报错
date:       2018-10-07
author:     Robot
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - Mybatis学习
---


# Mybatis中`mapper`代理方式报错

- 在使用Mybatis的mapper代理中的一个例子报错:

> org.apache.ibatis.binding.BindingException: Type interface com.mybatis.mapper.PersonMapper is not known to the MapperRegistry.

分析: 在运行这个例子中,`mapper.xml`文件单独写在了一个xml文件中,所以应该是`namespace`出了错, 仔细看了我的`namespace`路径发现,并没有把`com.mybatis.mapper.PersonMapper`这个接口的全路径写进去, 而是把这个接口上一层包名写进去 ,导致了错误
