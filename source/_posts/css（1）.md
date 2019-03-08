---
title: css（1）
date: 2018-11-21 21:27:04
tags: [css]
---
## 速记

1. 竖直方向上的margin会合并
但是 加上
Overflow:hidden
border-top:1px
padding-top:1px
display:inline-block
display:table
display:flex的话就不会合并
2. display:list-item
元素li本来是有小圆点的
因为它默认是display:list-item
改了display圆点会消失

3. position:absolute会改变元素的display
原先的display:inline或display:inline-block，会变成display:block

4. fixed定位的元素
如果父元素有transform:scale(0.9)
那么fixed定位的元素也会缩小，并且相对于父元素定位

## 请写出一行文本过长就变成省略号的例子
```html
<!DOCTYPE html>
<html lang="zh-hans">

<head>
    <title></title>
    <style>
        .test {
            width: 80px;
            text-overflow: ellipsis;
            overflow: hidden;
        }
    </style>
</head>

<body>
    <div class="test">
        asdp;oqwejaskljfdnas;lfoqjewrfqwraqertgataertga
    </div>
</body>

</html>
```

## 请写出「姓名」与「联系方式」两端对齐的例子

```html
<!DOCTYPE html>
<html lang="zh-Hans">

<head>
    <title></title>
    <style>
        span {
            border: 1px red solid;
            width: 5em;
            display: inline-block;
            text-align: justify;
        }

        span::after {
            content: '';
            display: inline-block;
            width: 100%;
        }
    </style>
</head>
<body>
    <div class="test">
        <span>姓名</span> <br>
        <span>联系方式</span>
    </div>
</body>
</html>
```

## 请写出一个高 40px 的 div，里面的文字垂直居中

```html
<!DOCTYPE html>
<html lang="zh-Hans">

<head>
    <title></title>
    <style>
        .test {
            line-height: 24px;
            padding: 8px;
            outline: 1px red solid;
        }
    </style>
</head>
<body>
    <div class="test">我是文字</div>
</body>
</html>
```

## 请写出多行文本超出部分变成省略号的例子

```html
<!DOCTYPE html>
<html lang="zh-Hans">

<head>
    <title></title>
    <style>
        .test {
            border: 1px red solid;
            display: -webkit-box;
            -webkit-line-clamp: 3;
            -webkit-box-orient: vertical;
            overflow: hidden;
        }
    </style>
</head>

<body>
    <div class="test">c
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
        z
        x
        c
        q
        a
        w
        e
        r
        a
        s
        f
        z
        x
        c
        v
        f
        z
        x
    </div>
   
</body>

</html>
```