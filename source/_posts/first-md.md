---
title: My First Blog
date: 2019-04-02 14:12:21
categories:
- Diary
tags:
- 随笔
---

## 第一个博客，要好好加油。

今天我试着玩了一下llvm的jit例子,但是在运行后却得到了一个error.
在网上到处找了一下，发现在INITIALIZE TARGET 后添加以下的代码可以解决我的问题。
{% codeblock lang:c++ %}
LLVMInitializeNativeAsmPrinter();
LLVMInitializeNativeAsmParser();
{% endcodeblock %}
奇怪为什么官方的代码会有问题。