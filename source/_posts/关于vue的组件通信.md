---
title: 关于vue的组件通信
date: 2019-05-05 21:26:46
tags: [Vue]
---
## 父子间的组件通信
今天来总结一下Vue中的组件通信,参考了官方教程和某些博客
父子间的通信有两种，一种是从父到子，另一种是从子到父
### 从父到子
一般使用props
```javascript
Vue.component('blog-post', {
  props: ['postTitle'],
  template: '<h3>{{ postTitle }}</h3>'
})

<blog-post post-title="hello!"></blog-post>
```
### 从子到父
使用emit
```javascript
// 父组件
<single-address @edit-address="editAddress"></single-address>
```
```javascript
// 子组件
methods: {
 editAddress () {
  this.$emit('edit-address', false)
 }
}
```
## 兄弟间的组件通信
使用event bus
```javascript
var bus = new Vue()
// 组件A
bus.$emit('id-selected', 1)
// 组件B
bus.$on('id-selected', function (id) {
 console.log(id)
})
```
## 祖孙间的组件通信
依赖注入,使用 provide 和 inject
```html
<!-- 组件结构 -->
<google-map>
  <google-map-region v-bind:shape="cityBoundaries">
    <google-map-markers v-bind:places="iceCreamShops"></google-map-markers>
  </google-map-region>
</google-map>
```

```javascript
// 组件google-map内部
// provide 选项允许我们指定我们想要提供给后代组件的数据/方法。在这个例子中，就是 <google-map> 内部的 getMap 方法
provide: function () {
  return {
    getMap: this.getMap
  }
}
```
```javascript
//然后在任何后代组件里，我们都可以使用 inject 选项来接收指定的我们想要添加在这个实例上的属性
inject: ['getMap']
```


## 另外一些方法
```javascript
this.$root
```
```javascript
this.$parent
```
```javascript
this.$children
```
```javascript
this.$refs
```
