---
title: js中的函数
date: 2018-11-03 21:00:10
tags: [javascript, 函数]
---

## 函数的五种声明方式

1.具名函数
```javascript
function x(input1,input2){
    return undefined
}
```

2.匿名函数
```javascript
var x = function  (input1, input2){
    return undefined
}

x.name // 'x'
```

3.具名函数赋值
```javascript
var x = function  y(input1, input2){
    return undefined
}

x.name // 'y'
```


4window.Function

```javascript
var x = new Function('x','y','return x+y')
x.name // "anonymous"
```


5箭头函数

```javascript
f= (x,y)=>{return x+y}
```



## js不一致性 

```javascript
function y(){}
console.log(y) //y(){}'
```
```javascript
var x = function y(){}

console.log(y) //报错
```

## 常见考点

### 作用域
```javascript
var a = 1
function f(){
    function f1(){
        var a = 3
    }
    var a = 2
}

f.call()
console.log(a) //1
```
log结果是1

```javascript
var a = 1
function f(){
    function f1(){
        var a = 3
    }
    var a = 2
}

f.call()
console.log(a) //1
```

-------


### 变量提升
```javascript
function f(){
    console.log(a)
    var a = 2
}

f.call() // a是undefined
```

这里涉及到变量提升，变量提升后的代码是这样的
```javascript
function f(){
    var a
    console.log(a)
    a = 2
}

f.call() // a是undefined
```
### 闭包

```javascript
function sum(a){
    function wrapper(b){
        return a + b
    }
    return wrapper
}

sum.call(4).call(3) // 7
o = sum(8) //返回一个函数
o(2)  // 10
```

闭包就是一个函数能引用到它作用域外的变量
这里 函数 o 依然可以引用到 8



