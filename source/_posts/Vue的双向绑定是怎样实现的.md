---
title: Vue的双向绑定是怎样实现的
date: 2019-05-08 22:03:59
tags: [Vue]
---

# 大概思路
vue数据双向绑定是通过数据劫持结合发布者-订阅者模式的方式来实现的，
代码大概分为三个部分：Observer、Watcher、Compile
## Observer
Observer主要用到了一个api叫 defineProperty，这个方法可以劫持一个对象的属性，操控它的getter和setter
什么叫getter、setter?看代码。
```javascript
var Book = {}
var name = '';
Object.defineProperty(Book, 'name', {
  set: function (value) {
    name = value;
    console.log('你取了一个书名叫做' + value);
  },
  get: function () {
    return '《' + name + '》'
  }
})
 
Book.name = 'vue权威指南';  // 你取了一个书名叫做vue权威指南
console.log(Book.name);  // 《vue权威指南》
```
可以看到，当我们对book的属性name进行赋值时，它会执行
```javascript
  set: function (value) {
    name = value;
    console.log('你取了一个书名叫做' + value);
  },
```
当我们访问Book.name时，它会执行
```javascript
  get: function () {
    return '《' + name + '》'
  }
```

这就是所谓的getter和setter。
通过这个api我们就可以实现 data 到 view的单向绑定。

要实现view到data的绑定，在dom节点上绑定事件就可以了

### 