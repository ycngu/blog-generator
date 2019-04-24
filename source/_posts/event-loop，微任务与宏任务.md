---
title: event-loop，微任务与宏任务
date: 2019-04-14 23:00:01
tags: [javascript]
---

## 代码为啥会这样？

很多时候我都对下列代码一脸懵逼

```javascript
setTimeout(function(){
    console.log('1')
})

new Promise(function(resolve){
    console.log('2')
    resolve()
}).then(function(){
    console.log('3')
})

console.log('4')
```

问：控制台以什么样的顺序打出console.log中的数字。

半桶水晃荡的前端（我）会说： 2 / 4 / 1 / 3
这是错的！

## js执行机制

关键在于js的执行机制

先来看图

![2.jpg](/images/eventloop/2.jpg)
在js中：
- 同步和异步任务分别进入不同的执行"场所"，同步的进入主线程，异步的进入Event Table并注册函数。
- 当指定的事情完成时，Event Table会将这个函数移入Event Queue。
- 主线程内的任务执行完毕为空，会去Event Queue读取对应的函数，进入主线程执行。
- 上述过程会不断重复，也就是常说的Event Loop(事件循环)。

也就是说，在上面一节的代码中，这两个同步任务会先被执行：
```javascript
new Promise(function(resolve){
    console.log('2')
    resolve()
})

console.log('4')
```

所以控制台会先打出 2 和 4

至于 1 和 3谁会先被控制台打出，就要看下图了：

![1.jpg](/images/eventloop/1.jpg)

宏任务微任务这两个名词的解释是：
- macro-task(宏任务)：包括整体代码script，setTimeout，setInterval
- micro-task(微任务)：Promise，process.nextTick

先执行宏任务，结束后判断有没有微任务，没有就执行宏任务，有就执行微任务，最后都是开始执行新的宏任务，一直循环。

以这个代码为例：

```javascript
setTimeout(function(){
    console.log('1')
})

new Promise(function(resolve){
    console.log('2')
    resolve()
}).then(function(){
    console.log('3')
})

console.log('4')
```

- 这段代码片段是宏任务，从上到下执行
- 碰到setTimeout， 将其注册分发到宏任务Event Queue。
- 碰到new Promise， 执行，控制台打出 ‘2’，then函数注册分发到微任务Event Queue。
- 碰到console.log ,执行控制台打出 ‘4’
- 一个宏任务结束，查看有没有微任务可以执行，好，有一个then函数在微任务Event Queue里，执行，控制台打出 ‘3’
- 一轮事件循环结束，从新的宏任务Event Queue开始，也就是setTimeout,控制台打出 ‘1’。

## 好记性不如烂笔头，特此记录！






