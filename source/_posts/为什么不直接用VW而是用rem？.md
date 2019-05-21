---
title: 为什么不直接用VW而是用rem？
date: 2019-05-21 18:56:24
tags:
---

# 为什么不直接用VW而是用rem？

突然想到了这个问题，自己试着解答一下

## vw和rem的差异
VW是根据视口宽度而定的,1vw等于视口宽度的1%
rem则是依据html元素的font-size大小而定，在rem动态方案中，会让html的font-size等于视口宽度，变相实现vw的效果（rem方案一般在窗口resize时会改变html的font-size）

PS:以前我在chrome使用vw，窗口resize，但是vw值并没有改变，现在试了下，vw会随着窗口resize改变。

## rem和vw的兼容性
rem的兼容性比vw的兼容性好，看下图
![rem-suit.jpg](source/_posts/为什么不直接用VW而是用rem？/rem-suit.png)
![vw-suit.jpg](source/_posts/为什么不直接用VW而是用rem？/vw-suit.png)