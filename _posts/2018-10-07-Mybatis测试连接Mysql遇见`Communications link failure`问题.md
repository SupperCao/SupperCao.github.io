---
layout:     post
title:      Mybatis测试连接Mysql遇见`Communications link failure`问题
subtitle:   Mybatis的异常
date:       2018-10-07
author:     CJ
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - Mybatis学习
---


# Mybatis测试连接Mysql遇见`Communications link failure`问题

#### 问题描述:<br/>
- 使用mybatis测试连接mysql遇见如下报错:<br/>

> ### Error querying database.  Cause: com.mysql.jdbc.exceptions.jdbc4.CommunicationsException: Communications link failure
The last packet sent successfully to the server was 0 milliseconds ago. The driver has not received any packets from the server.
### The error may exist in User.xml
### The error may involve MybatisMaper.FindUserById
### The error occurred while executing a query
### Cause: com.mysql.jdbc.exceptions.jdbc4.CommunicationsException: Communications link failure

百度了各种问题认为最有可能的问题是:<br/>

1）大量数据访问情况下，mysql connection连接有可能失效 
 
2）长时间不妨问，connection会失效

#### 解决方案: <br/> 
```
（1）使用JDBC URL中使用autoReconnect属性，url添加&autoReconnect=true&failOverReadOnly=false <br/>
（2）修改MySQL的参数. /etc/my.cnf 添加 [mysqld]
    wait_timeout=31536000
    interactive_timeout=31536000
（3）重启mysql 
    service mysql restart

```

<br/>

但是我最后的解决方法并不是如上,而是自己粗心忘记在`url`后面加上`//localhost:3306`
![](https://ws2.sinaimg.cn/large/006tNbRwgy1fvzqaa4s8xj30nq04i409.jpg)

最后我是改为 `<property name="url" value="jdbc:mysql://localhost:3306/mybatis?characterEncoding=utf-8" />` 就没有报错了
      