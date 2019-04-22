---
title: 使用java 储存Sql Server 精确到毫秒的datetime
date: 2019-04-22 15:35:12
categories:
- Diary
- Program
tags:
- 随笔
- Program
- java
- sqlserver
- datetime
---
# 使用java 储存Sql Server 精确到毫秒的datetime
使用SimpleDateFormat,pattern 设置为"yyyy-MM-dd HH:mm:ss.SSS",格式化java.util.Date.
将生成的字符串插入sql server.
取date数据应该用timestamp。
{% codeblock lang:java %}
SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss.SSS");
String date = dateFormat.format(new Date());
{% endcodeblock %}
