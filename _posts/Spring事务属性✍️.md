---
layout:     post
title:      Spring事务属性✍️
subtitle:   
date:       2018-07-15
author:     CJ
header-img: img/home-bg-art.jpg
catalog: true
tags:
    - Spring学习
    
---

## Spring事务属性✍️
![](https://ws3.sinaimg.cn/large/006tKfTcgy1ftav5btsi8j30xe0gotmw.jpg)

## 事务读取类型说明
- 脏读:

 > 事物没提交,提前读取
- 不可重复性：

 > 两次读取的数据不一致
- 幻读
 
 > 事物不是独立执行时发生的一种非预期现象
 
 
## 事物隔离级别
![](https://ws2.sinaimg.cn/large/006tKfTcgy1ftavcfj05yj30x00fhwpn.jpg)
 
## 事物是否只读
- 利用数据库事物的"只读"属性,进行特定优化处理
## 设置"只读" 注意:
- 事物是否`只读` 属性, 不同的数据库厂商支持不同
- 通常而言： 只读属性的应用要参考厂商的具体支持不同

## 事物超时
- 事物超时就是事物的一个定时器,特定的时间内事物如果没有执行完毕, 那么就会自动回滚, 而不是一直等待结束

##  事物回滚
- 默认情况下, 事物只有遇到运行期异常时才会回滚, 而在检查型异常不会回滚

## 事物接口
![](https://ws2.sinaimg.cn/large/006tKfTcgy1ftawb0talrj30pt0f7gvh.jpg)

 
 