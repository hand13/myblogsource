---
title: spring 整合mybatis 无法解析占位符
date: 2019-04-26 09:28:22
categories:
- Diary
- Program
tags:
- 随笔
- Program
- java
- spring
- mybatis
---
# spring 整合mybatis 无法解析占位符
整合spring 与mybatis 发现用MapperScannverConfigurer自动配置Mapper时，datasource 无法解析占位符。
代码如下
{% codeblock lang:xml %}
 <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource"
          p:driverClassName="${datasource.driver}"
          p:url="${datasource.url}"
          p:username="${datasource.username}"
          p:password="${datasource.password}"
          p:defaultAutoCommit="false"
          destroy-method="close"/>

    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean"
        p:dataSource-ref="dataSource" p:configLocation="classpath:mybatis.xml"
        p:mapperLocations="classpath:mapper/*.xml"/>

    <bean id="sqlSessionTemplate" class="org.mybatis.spring.SqlSessionTemplate">
        <constructor-arg name="sqlSessionFactory" ref="sqlSessionFactory"
                         index="0"/>
    </bean>

    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer"
         p:sqlSessionFactory-ref="sqlSessionFactory"
          p:basePackage="com.superdata.data.dao"/>
{% endcodeblock %}
经过百度上的一顿操作之后我我了解到应该是**Confirurer 的加载在placeholder之前，导致datasource直接使用了
占位符而不是解析后的字符串**。

要解决这个问题可以将Configurer 的配置中的 *p:sqlSessionFactory-ref="sqlSessionFactory"* 删除。
