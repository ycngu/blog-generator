---
title: vue的数组更新源码解析
date: 2019-07-13 12:24:03
tags: [vue]
---
# 问题:在vue里如何进行数组更新
Vue的[文档](https://cn.vuejs.org/v2/guide/list.html#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9)里已经说明了

由于 JavaScript 的限制，Vue 不能检测以下数组的变动：
- 当你利用索引直接设置一个数组项时，例如：vm.items[indexOfItem] = newValue
- 当你修改数组的长度时，例如：vm.items.length = newLength

vue里要让数组更新，使用的是Vue.set方法。

但是网上的很多文章里没有告诉我们Vue.set方法究竟干了什么。

下面我们看源码

# 源码:set部分
Vue2.6的set方法源码：
```javascript
/**
   * Set a property on an object. Adds the new property and
   * triggers change notification if the property doesn't
   * already exist.
   */
  function set (target, key, val) {
    if (isUndef(target) || isPrimitive(target)
    ) {
      warn(("Cannot set reactive property on undefined, null, or primitive value: " + ((target))));
    }
    if (Array.isArray(target) && isValidArrayIndex(key)) {
      target.length = Math.max(target.length, key);
      target.splice(key, 1, val);
      return val
    }
    if (key in target && !(key in Object.prototype)) {
      target[key] = val;
      return val
    }
    var ob = (target).__ob__;
    if (target._isVue || (ob && ob.vmCount)) {
      warn(
        'Avoid adding reactive properties to a Vue instance or its root $data ' +
        'at runtime - declare it upfront in the data option.'
      );
      return val
    }
    if (!ob) {
      target[key] = val;
      return val
    }
    defineReactive$$1(ob.value, key, val);
    ob.dep.notify();
    return val
  }
```
这里只关注关于数组的部分：
```javascript
if (Array.isArray(target) && isValidArrayIndex(key)) {
      target.length = Math.max(target.length, key);  //取length和index中大的那一个，这里key是indexOfItem
      target.splice(key, 1, val);
      return val
}

//使用时就是Vue.set(vm.items, indexOfItem, newValue)
```
当传入的target是数组且indexOfItem正常时，调用vue包装过的splice方法然后return val。

上面说到vue不能检测数组的变动，set方法其实就是用vue包装过的splice变异方法来进行数组更新。

这里请看vue[变异方法](https://cn.vuejs.org/v2/guide/list.html#%E5%8F%98%E5%BC%82%E6%96%B9%E6%B3%95-mutation-method)的文档

那么splice变异方法又是怎么做到的呢

# 源码：变异方法部分

包装数组方法的源码：

```javascript
var methodsToPatch = [
    'push',
    'pop',
    'shift',
    'unshift',
    'splice',
    'sort',
    'reverse'
];

methodsToPatch.forEach(function (method) {
    // cache original method
    var original = arrayProto[method];
    //def函数是vue稍微封装了一下Object.defineProperty
    def(arrayMethods, method, function mutator () {
      var args = [], len = arguments.length;
      while ( len-- ) args[ len ] = arguments[ len ];

      var result = original.apply(this, args);
      var ob = this.__ob__; //ob是vue自己封装的observer对象，要想了解请去网上看vue双向绑定源码的解析
      var inserted;
      switch (method) {
        case 'push':
        case 'unshift':
          inserted = args;
          break
        case 'splice':
          inserted = args.slice(2);
          break
      }
      if (inserted) { ob.observeArray(inserted); }
      // notify change
      ob.dep.notify();
      return result
    });
  });
```

```javascript
  Observer.prototype.observeArray = function observeArray (items) {
    for (var i = 0, l = items.length; i < l; i++) {
      observe(items[i]);
    }
  };
```

未完待续...



