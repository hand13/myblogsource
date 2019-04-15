---
title: 使用turbo-jpeg 解码jpeg 图片，再用SDL2显示。
date: 2019-04-15 11:01:01
categories:
- Diary
- Program
tags:
- 随笔
- Program
- cpp
- SDL2
- jpeg
---
# 使用turbo-jpeg 解码jpeg 图片，对解码后的数据进行一些处理，再用SDL2显示。
使用turbo时，应该先调用对应的init方法进行初始化，在解码/编码。
在使用过程中可以compressHeader来获取图片的大体信息。
sdl2显示RGB内存数据时，可以先creatergbsurface来得到sufaface,在通过surface
来创建texture,最后通过sdl 显示texture(renderpresent).