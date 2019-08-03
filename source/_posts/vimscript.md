---
title: vim 与 vimscript
date: 2019-08-03 09:46:25
categories:
- Diary
tags:
- Program
- vim
---
###### 本人是半桶水，如果有谁不幸看到这篇文章建议点X
##### 前言： vim，上古神器,编辑器之神.
我所知道的常用的ide与编辑器基本都有vim模式(当然都没有vimscript解析,只有vim 风格的按键模式.所以说还是用vim啦,毕竟插件骚操作多).
一套按键模式，走遍天下都不怕,妈妈再也不用担心我记不住快捷键了,不学不是人。
## vim 常用 与vimscript基础
vim 的配置文件为$HOME/.vimrc,通过将路径添加到rpt变量中来改变vim加载vimscript的路径。
常见对象有buffer,window,tab。编辑文件时之间操作的是buffer,通过指令(w)保存后才会写入到
对应的文件里.
### vim 工作时有四种模式
1. insert模式:在此模式下进行字符输入,可以按i进入.
2. visual模式:在模式下可以选择字符,按v,V进入.
3. normal模式:在此模式可以进行各种文本操作,如移动，删除,esc进入.
4. command模式:normal 模式下按:进入,command 模式下输入的指令与vimscript语法一致
### vim 指令
normal 模式下 [range]com,range 表范围，一般为行号,逗号分隔：
hjkl进行移动操作,x,d进行删除操作,r替换操作之类
### 通过set 可以改变vim的一些option:
如 set number--显示行号，set nonumber--不显示行号
set number? ---显示设置的number的值.
### 通过map 来进行按键映射.
map 分为3种,分别对应于三种模式,imap,vmap.nmap.
在map 前加上nore可以关闭递归求值,inoremap.vnoremap.nnoremap
实例:inoremap jk <ESC>,insert 模式下将jk映射值esc键
###  vimscript
1. 各种c系控制流程语句.if---endif,while---endwhile,for----endfor
2. 函数,function---endfunction
3. let 绑定变量.变量通过加前缀来表示作用域，如s,a,g,b,l
let l:filename = xxx.txt
##### 先这样吧，东西太多，还是直接看资料来的实在[learn vimscript the hard way](http://learnvimscriptthehardway.stevelosh.com/)