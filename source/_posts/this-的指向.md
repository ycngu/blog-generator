---
title: this 的指向
date: 2018-11-11 17:38:57
tags:
---
在做下面两道题时有疑惑

后来运行了代码就清楚了，特此记录



```javascript
window.name = 'window name'

var obj = {
    name: 'ycngu',
    f: function () {
        console.log(this.name)
    }
}

obj.f() // 'ycngu'
```
```javascript
window.name = 'window name'

let obj2 = {
    name: 'obj name',
    f: () => {
        console.log(this.name)
    }
}

obj2.f() // 'window name'
```
上面两个函数的执行结果分别是'ycngu'和'window name'

第一个函数obj调用的时候实际上是这样的

obj.f.call(obj)

call的第一个参数就是this，在这里是obj

第二个函数里f这个函数是箭头函数，函数调用时箭头函数里的this指向的是widow

