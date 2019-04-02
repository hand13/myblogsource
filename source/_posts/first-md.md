---
title: My First Blog
date: 2019-04-02 14:12:21
categories:
- Diary
tags:
- 随笔
---

## 第一个博客，要好好加油。

Today,I try to compile llvm jit example.
unfortunately I got a error.
after place this code
{% codeblock lang:c++ %}
LLVMInitializeNativeAsmPrinter();
LLVMInitializeNativeAsmParser();
<% endcodeblock %>
before the initialize target code,I solved my problem.
