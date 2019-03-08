---
title: JS里的数据类型转换
date: 2018-10-14 19:40:37
tags: [javascript, 数据类型转换]
---
## js数据类型
复习
上回说过，javascript有七种数据类型，分别是：
 * number (小数和整数，如1，1.2324)
 * string （字符串，如 'hello'）
 * boolean （true和false） 
 * symbol (es6新数据类型)
 * object (注意array和function都是object)
 * null （空值）
 * undefined （未定义）
<!--more-->
那它们之间怎么转换呢？
## string
可以使用obj.toString(),也可以加上一个空字符串或使用String函数，但obj.toString()有局限性。
```javascript
//number
1.toString() //'1'

//boolean
b = true
b.toString() //'true'
b + '' //'true'

//symbol 这个不用记
s = Symbol('Symbol')
s.toString() // "Symbol(symbol)"

s + '' //Cannot convert a Symbol value to a string

//null
null.toString() // TypeError: Cannot read property 'to' of null

null + '' // "null"

//undefined
undefined.toString() //Cannot read property 'toString' of undefined

undefined + '' //"undefined"

//object
object = {name:'ycngu'} //"[object Object]"

object + '' //"[object Object]"
```

## boolean

Boolean函数用来返回布尔值
js中有五个值要记住，这五个值输入Boolean函数会返回false,称为**falsy**
（还有其他值，但记住这些就够了 ）
分别是：
```javascript
Boolean(null)
Boolean(undefined)
Boolean('') // 空字符串
Boolean(0) // number
Boolean(NaN) // number
//以上全部返回false
```
**要注意的是，所有的Object都是true,包括function和array**
```javascript
function f(){}
arr = []
obj = {}
Boolean(f) //函数
Boolean(arr) //数组
Boolean(obj) //对象
//以上全部返回true
```
有一种偷懒方法可以方便的得知true和false
```javascript
!! true // true
!! {} // true
!! 0 //false
```
## number
四种方法
- Number()
- parseInt()
- parseFloat()
- 减去0
- 取正 +'1.23' // 1.23
一般都是把string转为number
下面说一下值得提的点
```javascript
true + true // 等于2 ！！！
true * 3 // 等于3 
//也就是说 true和数字进行计算的时候等于1

false + 3 //等于 3
false * 3 //等于0
//也就是说 false和数字进行计算的时候等于0

undefined + 0 // NaN
null + 1 // 1

parseInt('123s') // 123
parseInt('123lsdasd1213') // 123
//parseInt函数有两个参数，一个是解析的值，另一个是确定几进制的值，默认是10进制，parseInt会尽力解析值，直到不能解析，所以这里得到的是 123
```



