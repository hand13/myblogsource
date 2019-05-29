---
title: 编写idea 插件，已通过插件来使用lua 间接控制idea
date: 2019-05-29 11:11:20
categories:
- Diary
- Program
tags:
- 随笔
- Program
- idea
- plugin
---

#### 使用了idea这么久，总觉得Idea缺少自动脚本控制的机制（或许是我自己不知道），于是决定自己写一个插件来通过载入lua脚本控制idea。
##### 通过这个项目顺便学习一下idea plugin 的制作与lua.
关于idea plugin 的api可以参考[IntelliJ Platform SDK](http://www.jetbrains.org/intellij/sdk/docs/welcome.html)
java通过luaj 来使用lua。
[这是我的github项目](https://github.com/hand13/idealuascript.git)
现在还不是很完善，后面会持续更新。