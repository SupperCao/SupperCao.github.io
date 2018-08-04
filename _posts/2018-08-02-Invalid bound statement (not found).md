# Invalid bound statement (not found)
解决方法:
> 首先检查 namespace的包名是否错误,以及名字是否有写错

最重要的是在整合的时候application.xml文件中包含Mapper.xml文件

```
      <!-- 创建mybatis的SqlSessionFactory -->
        <bean id="sqlsessionfactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <!-- 指定数据源（） -->
        <property name="dataSource" ref="datasource"></property>
        <!-- 指定数mybatis核心配置文件 -->
         <property name="mapperLocations" value="classpath:com/ts/xyts/emall/mapper/*Mapper.xml" />  
        <property name="configLocation" value="classpath:mybatis/mybatisConfig.xml"></property>
        </bean>

```