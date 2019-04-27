---
title: 三行说明rem自适应布局方案
date: 2019-04-24 20:49:08
tags: ['javascript','布局']
---

## 说明
rem自适应布局方案，其要点是让css中的rem单位根据页面的宽度的变化而变化
而 rem 的大小 等于 html的font-size大小。

那么，让 html的font-size 等于 页面的宽度就能实现目标了。

## 代码

```javascript
let width = document.documentElement.clientWidth ||document.body.clientWidth
//这一行获取当前页面的宽度

let html = document.querySelector('html')
//这一行获取html dom

html.style.fontSize = width /10 + 'px'    
//这一行把html的fontsize设置成 width的十分之一，使用vw时1vw就等于页面的十分之一宽。
```
