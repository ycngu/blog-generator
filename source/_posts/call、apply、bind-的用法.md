---
title: call、apply、bind 的用法
date: 2018-11-27 21:03:52
tags: [javascript,语法]
---

call、apply、bind这三个的作用都是改变函数运行时this的指向

## call
call方法第一个参数是要绑定给this的值,从第二个值开始是传入的参数
```javascript
function fun(a){
    console.log(this,a)
}

fun.call(undefined,1)
```
在开发者工具输入以上代码会出现window和1，这是因为浏览器在默认情况下如果第一个参数是null或者undefined,this就会是window。使用严格模式(use strict)才会是undefined。

输入多个参数的函数是这样的：
```javascript
function fun(a,b,c){
    console.log(this,a,b,c)
}

fun.call(undefined,1,2,3) // console显示1 2 3
```

## apply
apply方法的用法和call方法差不多，不过apply方法的第二个参数是一个参数数组
```javascript
var arr = [1,2,3,89,46]
var max = Math.max.apply(null,arr)  //arr是一个数组，函数运行结果是89
```

假设有两个个函数fn1，fn2，它们的作用是一样的,call和apply两种方法的对比是这样的：
```javascript
fn1.call(undefined,1,2,3,4,5)
fn2.apply(undefined,[1,2,3,4,5])
```
## bind
bind方法call很相似，第一个参数是this的指向，从第二个参数开始是接收的参数列表，区别在于bind方法返回值是函数以及bind接收的参数列表的使用。
```javascript
var obj = {
    name: 'Dot'
}

function printName() {
    console.log(this.name)
}

var dot = printName.bind(obj)
console.log(dot) // function () { … }
dot()  // Dot
```
bind 方法不会立即执行，而是返回一个改变了上下文 this 后的函数。而原函数 printName 中的 this 并没有被改变，依旧指向全局对象 window。

```javascript
function fn(a, b, c) {
    console.log(a, b, c);
}
var fn1 = fn.bind(null, 'Dot');

fn('A', 'B', 'C');            // A B C
fn1('A', 'B', 'C');           // Dot A B
fn1('B', 'C');                // Dot B C
fn.call(null, 'Dot');      // Dot undefined undefined
```
call 是把第二个及以后的参数作为 fn 方法的实参传进去，而 fn1 方法的实参实则是在 bind 中参数的基础上再往后排。