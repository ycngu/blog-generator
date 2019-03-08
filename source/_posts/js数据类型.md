---
title: javascript数据类型
date: 2018-10-13 14:02:31
tags: [javascript]
---


## js数据类型
javascript有七种数据类型，分别是：
 * number (小数和整数，如1，1.2324)
 * string （字符串，如 'hello'）
 * boolean （true和false） 
 * symbol (es6新数据类型)
 * object (注意array和function都是object)
 * null （空值）
 * undefined （未定义）
<!--more-->
## number
JavaScript 内部，所有数字都是以64位浮点数形式储存,包括整数。
所以会有下面的情况
```javascript
var a = 1
var b =1.0

a == b //true

1.1 - 1 // 0.10000000000000009
//1.1 以64位浮点数形式储存，所以会出现这样的结果
```
**so注意,涉及到小数的运算都要特别小心**

NaN是 JavaScript 的特殊值，表示“非数字”（Not a Number），主要出现在将字符串解析成数字出错的场合.
```javascript
NaN

1 * 'kk' //NaN
```  

以下是各进制在js中的表示方法
```javascript
24//十进制
1.3e4//十进制，科学计数法
0b11//二进制，0b开头
011//八进制，以0开头
0xff//十六进制，0x开头
```

## string
字符串有多种定义的方式
```javascript
'hello' //用单引号包起来
"world" //用双引号包起来

`hello
world` //多行字符串写法一，用反引号包起来 
```
问：反引号括起来的helloworld的length是多少？
答：11，因为 **包含了回车！** 千万要注意。

```javascript
//多行字符串写法二
var w1 = '12345 \    
          67890'

var w2 = '12345 \
          67890'
```
问：上面的代码中，w1和w2有什么区别？
答：按 ctrl+a ，你会看到 w1的12345后面紧跟着空格，w2则没有，w1会报错！！！坑死人不偿命

如果一定要换行，正确的写法是

```javascript
var w1 = '12345' +
         '67890'
```

## boolean
boolean只有true和false两个值
通常和if else 和 && ||等运算符一起使用
```javascript
if(true){
    //执行这里的代码
}

if(false){
    //不执行这里的代码
}
```

```javascript
true && false //false

true || false //true
```

## null 和 undifined

这两个都表示什么都没有
js之父承认这是他设计错了（手动滑稽）

```javascript
var a

// a的值为undefined
```

> **如果一个变量没有赋值，会被js赋值为undefined
如果有一个object对象，现在不想给值，推荐初始化成null
如果有一个非object对象，现在不想给值，推荐初始化成undefined**

## object

以上都属于基本类型，而object是复杂类型，由简单类型组成

```javascript
var name = 'joe'
var age = 18
var gender = 'male'
//简单类型

var person = {
    name: 'joe',
    age: 18,
    gender: 'male'
}
//复杂类型,由简单类型组成
```
**注意这里有个坑**
```javascript
var name = 'xxxx'
person[name]
person['name']
```
问：person[name]和person['name']的值分别是多少？
答：前一个是undefined，后一个是 'joe'

person[name] //实际上是person['xxxx']


```javascript
function f(){}

typeof(f) //'function'
```
**如果用typeof函数去测f,那么会显示f的类型是function,实际上f的类型是objcet,谨记**
## symbol
> ES5 的对象属性名都是字符串，这容易造成属性名的冲突。比如，你使用了一个他人提供的对象，但又想为这个对象添加新的方法（mixin 模式），新方法的名字就有可能与现有方法产生冲突。如果有一种机制，保证每个属性的名字都是独一无二的就好了，这样就从根本上防止属性名的冲突。这就是 ES6 引入Symbol的原因。

以上是阮一峰老师的解释
更多知识请猛戳以下两个链接
http://es6.ruanyifeng.com/#docs/symbol
https://zhuanlan.zhihu.com/p/22652486

symbol类型通过symbol函数创建
```javascript
let a = symbol()
```
Symbol函数可以接受一个字符串作为参数，表示对 Symbol 实例的描述，主要是为了在控制台显示，或者转为字符串时，比较容易区分。
```javascript
let s1 = Symbol('foo');
let s2 = Symbol('bar');

s1 // Symbol(foo)
s2 // Symbol(bar)

s1.toString() // "Symbol(foo)"
s2.toString() // "Symbol(bar)"
```

