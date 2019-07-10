---
title: 来写一写jquery
date: 2018-11-13 10:29:55
tags: ['jquery','javascript']
---

## 1.初次尝试

第一个版本，简单地使用function声明函数,使用官方api封装两个函数

```javascript
function getSiblings(node) {
    //获得node的兄弟节点
    var allChildren = node.parentNode.children

    var array = {
        length: 0
    }

    for (let i = 0; i < allChildren.length; i++) {
        if (allChildren[i] !== node) {
            array[array.length] = allChildren[i];
            array.length += 1
        }
    }
    return array
}

function toogleClass(node, classes) {
    //开关函数，对于node，有class就移除class，没有class就添加class
    for (let key in classes) {
        var methodName = classes[key] ? 'add' : 'remove'
        node.classList[methodName](key)
    }
}
```
这样做有很大的缺点，万一别人也定义了一个getSiblings函数怎么办，听谁的？
所以要继续改进

## 2.一鼓作气 
为了解决函数名字重复的问题，在第一个版本的基础上，我们使用命名空间。
```javascript
window.ycdom = {}
ycdom.getSiblings = getSiblings
ycdom.toogleClass = toogleClass

//这样调用函数的时候就是：
var node = document.querySeletor('#x')
ycdom.getSiblings(node)
```
使用命名空间还可以提高辨识率，防止你写辣鸡代码 (。・∀・)ノ
## 3.再战江湖 
在上一个版本ycdom.getSiblings(node)这样的代码太长，而且视觉上node在后面，看代码时不容易知到node是哪个节点。

第三个版本，在Node原型上添加自己封装的函数。
```javascript
Node.prototype.getSiblings = function () {
    allChildren = this.parentNode.children
    //获得node的兄弟节点
    var array = {
        length: 0
    }

    for (let i = 0; i < allChildren.length; i++) {
        if (allChildren[i] !== this) {
            array[array.length] = allChildren[i];
            array.length += 1
        }
    }
    return array
}

Node.prototype.toggleClass = function (classes) {
    //开关函数，对于node，有class就移除class，没有class就添加class
    for (let key in classes) {
        var methodName = classes[key] ? 'add' : 'remove'
        this.classList[methodName](key)
    }
}
```
现在我们可以这样使用了:
**var node = document.querySeletor('#x')**
**node.getSinlings()**
这样用起来更方便，更舒服，但是在原型上添加东西的话是一种破坏，多人协作每个人都往原型添点东西不用多久就天下大乱了。还得改进。
## 4.最终版本
```javascript
window.jQuery = function (nodeOrSeletor) {
    let nodes = {}
    if (typeof nodeOrSeletor === 'string') {
        let temp = document.querySelectorAll(nodeOrSeletor)
        for (let i = 0; i < temp.length; i++) {
            nodes[i] = temp[i]
        }
        nodes.length = temp.length
    } else if (nodeOrSeletor instanceof Node) {
        nodes = {
            0: nodeOrSeletor,
            length: 1
        }
    }


    nodes.addClass = function (classes) {
        //当classes不是数组时，会报错，所以为了健壮性写了两段代码处理不同情况
        //这里默认参数是字符串或数组
        if (typeof classes === 'string'){
            for (let i = 0; i < nodes.length; i++) {
                nodes[i].classList.add(classes)
            }
        } else {
            classes.forEach(value => {
                for (let i = 0; i < nodes.length; i++) {
                    nodes[i].classList.add(value)
                }
            })
        }
    } 
    nodes.getText = function () {
        var texts = []
        for (let i = 0; i < nodes.length; i++) {
            texts.push(nodes[i].textContent)
        }
        return texts
    }
    nodes.setText = function (text) {
        for (let i = 0; i < nodes.length; i++) {
            nodes[i].textContent = text
        }
    }

    return nodes
}


window.$ = jQuery //相当于把jQuery命名为$
```

我们没有修改Node的原型。
定义了jQuery函数，这个函数返回对象nodes，nodes自带三个方法：getText setText addClass，最后一行
```javascript
window.$ = jQuery 相当于把jQuery命名为$
```
可以像下面这样使用
```javascript
var $div = $('div')
$div.addClass('red') // 可将所有 div 的 class 添加一个 red
$div.setText('hi') // 可将所有 div 的 textContent 变为 hi
```