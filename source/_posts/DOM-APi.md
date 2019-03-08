---
title: DOM APi
date: 2018-11-03 21:51:20
tags:
---
注：以下文字有很多来自阮一峰老师的js教程
## DOM

DOM 是 JavaScript 操作网页的接口，全称为“文档对象模型”（Document Object Model）。它的作用是将网页转为一个 JavaScript 对象，从而可以用脚本进行各种操作（比如增删内容）。

DOM 的最小组成单位叫做**节点（node）**。文档的树形结构（DOM 树），就是由各种不同类型的节点组成。每个节点可以看作是文档树的一片叶子。

节点的类型有七种。

> Document：整个文档树的顶层节点
> DocumentType：doctype标签（比如&lt;!DOCTYPE html>）
> Element：网页的各种HTML标签（比如&ltbody>、&lta>等）
> Attribute：网页元素的属性（比如class="right"）
> Text：标签之间或标签包含的文本
> Comment：注释
> DocumentFragment：文档的片段

## Node

浏览器提供一个原生的节点对象Node，上面这七种节点都继承了Node，因此具有一些共同的属性和方法。

Node接口属的性具体如下
>Node.nodeType
Node.nodeName
Node.nodeValue
Node.textContent
Node.baseURI
Node.ownerDocument
Node.nextSibling
Node.previousSibling
Node.parentNode
Node.parentElement
Node.firstChild，Node.lastChild
Node.childNodes
Node.isConnected

Node接口的方法如下
>Node.appendChild()
Node.hasChildNodes()
Node.cloneNode()
Node.insertBefore()
Node.removeChild()
Node.replaceChild()
Node.contains()
Node.compareDocumentPosition()
Node.isEqualNode()，Node.isSameNode()
Node.normalize()
Node.getRootNode()

## Nodelist

NodeList实例是一个类似数组的对象，它的成员是节点对象。通过以下方法可以得到NodeList实例。

>Node.childNodes
document.querySelectorAll()、document.getElementsByTagName()等节点搜索方法

NodeList是伪数组，可以使用length属性和forEach方法。但是，它不是数组，它的原型链上没有Array.prototype，不能使用pop或push之类数组特有的方法。

## HTMLCollection
HTMLCollection是一个节点对象的集合，只能包含元素节点（element），不能包含其他类型的节点。它的返回值是一个类似数组的对象，但是与NodeList接口不同，HTMLCollection没有forEach方法，只能使用for循环遍历。

返回HTMLCollection实例的，主要是一些Document对象的集合属性，比如document.links、docuement.forms、document.images等。

**HTMLCollection实例都是动态集合，节点的变化会实时反映在集合中。**

## ChildNode 接口

如果一个节点有父节点，那么该节点就继承了ChildNode接口。

Node接口的方法如下
> ChildNode.remove()
ChildNode.before()
ChildNode.after()
ChildNode.replaceWith()