---
title: Spring Redis Session
date: 2019-05-07 08:58:59
categories:
- Diary
- Program
tags:
- 随笔
- Program
- java
- spring
- redis
---
# 通过Spring Session实现Session的共享
1. 通过maven导入相关的依赖。
2. 在web.xml中添加如下Filter.
{% codeblock lang:xml %}
  <filter>
        <filter-name>springSessionRepositoryFilter</filter-name>
        <filter-class>org.springframework.web.filter.DelegatingFilterProxy</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>springSessionRepositoryFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
{% endcodeblock %}

3. 在spring 配置文件中导入如下bean
{% codeblock lang:xml %}
<bean class="org.springframework.session.data.redis.config.annotation.web.http.RedisHttpSessionConfiguration"/>
{% endcodeblock %}
4. 完成后多个application就可以访问共用session.


