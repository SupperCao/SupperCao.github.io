---
layout:     post
title:      java基础学习-转义字符
subtitle:   java基础
date:       2018-04-21
author:     BY
header-img: img/home-bg-art.jpg
catalog: true
tags:
    - java
    - java基础
---

# java基础学习-转义字符

> 转义字符是用于字符的操作，例如pringln(**ln**自带了换行操作), 例如:<br/>
> out.println("hello")<br/>
> out.println("World"), 则输出为上下两行文字 ,如果是out.print(),则不会换行。<br/>
> 但是要在out.print（）中换行的话就需要转义字符

<br/>
<br/>

| 转义字符    |   意义  |
| ------ | ------ | ------ |
|    \ n |  换行(换到当前位置移动到下一行开头) |
|    \ r |  回车（将当前位置移到本行开头）     |
|    \ t |  相当于Tab     |
|    \ b |  退格（将当前位置移到前一列）     |
|    \ f |  换页（将当前位置移到下页开头）     |
