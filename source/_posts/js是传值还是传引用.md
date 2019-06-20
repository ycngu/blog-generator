---
title: js是传值还是传引用?
date: 2019-04-17 21:46:39
tags: [javascript]
---
# 先说结论

<<javascript高级程序>>这本书上说，javascript是*按值传参*

但是javascript给人的感觉很古怪，一下让人觉得是传值，一下又让人觉得是传引用，name到底是怎么回事呢？

答案是传值。

## 为何
来看下面几道面试题，首先是基本类型number
```javascript
//第一题
var a = 1

function change1(a){
    a = 2
}

console.log(a) //输出 1
```

如果传的是引用，那么a的值就会被改变，很明显是传值，但这是基本类型number，如果是object呢？

```javascript
//第二题
var b = {
    name:'fire',
    age:'30',
}

function change2(b){
    b.name = 'water'
}

change2(b)

console.log(b.name)  //输出 water
```

说好的传值呢？怎么b.name被改变了？看下一题

```javascript
//第三题
var b = {
    name:'fire',
    age:30,
}

function change3(b){
    b = {
        name:'water',
        age:30,
    }
}

change3(b)

console.log(b.name)  //输出 fire
```

这下看上去还是传值，究竟是咋回事

这是因为js在传object这种复杂类型的时候，传的是 指向object的指针的拷贝

重点 指向object的指针的拷贝
重点 指向object的指针的拷贝
重点 指向object的指针的拷贝

所以<<javascript高级程序>>说js是按值传参也没错

因为传的是指针，所以第二题中 给b.name赋值会改变指针指向的对象的值， 函数外面的b的指针也是指向这个对象，所以值会改变

第三题中，change函数里的b被赋予一个新的对象，等于改变指针指向为一个新的对象，而不是改变旧对象里的值，所以外面的b的值还是fire

## 总结

复杂对象如object是传的指针的拷贝，也是传值
简单对象如number是传值

