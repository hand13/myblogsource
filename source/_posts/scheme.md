---
title: Scheme
date: 2019-07-06 08:47:26
categories:
- Diary
- Program
tags:
- 随笔
- Program
- hasell
---
# Scheme 笔记
## Scheme 是一个语法非常精简的函数式语言，作为lisp 语言的一份子同样也有着总多的实现。
我在学习Scheme的时候主要使用的是[Chez Scheme](https://github.com/cisco/ChezScheme.git).文档可以[参考](https://www.scheme.com/tspl4/),
这个实现已经开源在github上了.
### Scheme 的语法非常简洁，由S表达式构成,通常是(A B C)这样的形式。部分常用的数据结构存在字面量。可以使用宏定义自己的语法结构。
关键字主要是 define lambda:
1. 用来将值与变量绑定的define.
(define a 12)

(define a (+ 12 12))
2. 用来编写lambda 表达式的lambda.
(lambda (x) (+ x x))

(define b (lambda (x) (+ x x)))

(b 12)
3. let
4. 在scheme中函数的命名存在模式,!后缀意味着该函数可能
会改变状态，?意味着该函数会返回一个布尔值.
### 数据类型.
1. 数字，不区分浮点与整形.
2. 字符串.
3. 布尔类型.字面量 #f 为false,#t 为true.
4. 符号类型，以“ ' ”开头，scheme 不会对 ' 后面的符号求值.
(define w '(a b c d))
5. record类型.
6. port类型，用于IO.