---
title: css布局
date: 2018-10-03 23:20:07
tags: [javascript]
---

## 左右布局

左右布局常用float

**css:**
```css
    .clearfix::after{
        content: '';
        display: block;
        clear: both;
    }

    .child1{
        float:left;
    }

    .child2{
        float:right;
    }
```
**html:**
```html
    <div class="parents clearfix">
        <div class="child1"></div>
        <div class="child2"></div>
    </div>
```

这样的左右布局关键点在于给子元素添加左右浮动，给父元素添加clearfix

clearfix::after 是套路，记住就行了
<!--more-->
##左中右布局

左中右布局：有圣杯布局和双飞翼布局。
它们的特点都是左右两栏固定宽度,中间部分自适应。

下面这个是圣杯布局
**css:**
```css
    .container {
        padding: 0 200px 0 220px;
        overflow: hidden;
    }

    .left , .right , .middle {
        float: left;
        position: relative;	
        min-height: 130px;
    }

    .left{
        width: 200px;
        left: -200px;
        margin-left: -100%;
        background-color: green;
    }

    .middle{
        width: 100%;
        background-color: yellow;
    }

    .right{
        width: 220px;
        margin-left: -220px;
        right: -220px;
        background-color: blue;
    }
```
**html:**
```html
    <div class="container">
        <div class="middle"></div>
        <div class="left"></div>
        <div class="right"></div>
    </div>	
```

## 水平居中
方法1
在块级父容器中让行内元素居中
```css
    main{
        text-align:center;
    }
```
方法2
块级元素居中
```css
    main{
        margin: 0 auto;
    }
```
方法3
绝对定位实现水平居中
```css
    main{
        position: absolute; 
        width: 宽度值; 
        left: 50%; 
        margin-left: -(宽度值/2);
    }
```
方法4
利用css3新特性transform
```css
    main{
        position: absolute;
        left: 50%;
        transform: translateX(-50%);
    }
```

## 垂直居中

方法1
把line-height设置为容器div的高度就能使文字垂直居中，假设div高50px
```css
    main{
        line-height:50px;
    }
```

下面是抄的河大博文，先说一句河大牛逼！（只抄了我认为用起来很爽的）
细节请看：http://note.codermagefox.com/blog/post/magefox/centerItvertically

方法2
```css
    main{
        position:absolute; /*绝对定位*/
        top: 50%;/*向下移动父元素高度一半*/
        left:50%;/*向右移动父元素宽度一半*/
        transform: translate(-50%,-50%);
    }
```
方法3
使用VH
```css
    main{
        position:absolute; /*绝对定位*/
        top: 50%;/*向下移动父元素高度一半*/
        left:50%;/*向右移动父元素宽度一半*/
        transform: translate(-50%,-50%);
    }
```
方法4
用flex
```
<style>
    body{
        display: flex;
        min-height: 100vh;
        margin: 0;
    }
    main{
        margin:auto 0 auto 0;
    }
</style>
<body>
<main>
    <h1>A quick brown fox jump over the lazy dog</h1>
</main>
```
方法5
在方法4基础上加上
```css
    main{ 
        align-self:center; 
    } 
```

## 其它
```css
::nth-child(odd) // 选择单数的子元素
::nth-child(even) // 选择双数的子元素
::nth-child(1) // 选择第一个子元素
```

> * div高度由其内部文档流元素的高度总和决定

> * 文档流：文档内元素的流动方向

> * 内联元素从左往右流动，如果流动遇到阻碍，就换行
块级元素，每一个块级元素占一行

> * 内联元素  中文换行会被分，英文不会被分
word-break属性用来解决这个事情
Word-break:break-all / break-word

> * 内联元素根据基线对齐

> * 在html中回车会变成一个空格
