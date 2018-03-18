---
title: 关于class的一些总结
date: 2018-03-05 14:52:14
tags:
  - JS
---

- 类和模块的内部，默认就是严格模式

## 类和构造函数的区别

- **类原型对象上的方法是不可枚举的**，包括constructor构造方法
  ```js
    class Point {
      constructor(x, y) {}

      toString() {}

      toNumber(){}
    }

    Object.keys(Point.prototype);  // []
    Object.getOwnPropertyNames(Point.prototype);  // ["constructor", "toString", "toNumber"]
  ```
  上例所示，通过`Object.keys()`方法返回给定对象的可枚举属性组成的数组为空，通过`Object.getOwnPropertyNames()`方法返回了包括不可枚举属性组成的数组，其中三个元素都是不可枚举的

<!-- more -->

- **构造函数原型对象上的方法是可枚举的**，包括constructor构造方法
  ```js
    function Point2(x, y) {}

    Point2.prototype = {
      toString(){},

      toNumber(){}
    }

    Object.keys(Point2.prototype);  // ["toString", "toNumber"]
    Object.getOwnPropertyNames(Point2.prototype);  // ["toString", "toNumber"]
  ```


## 实例对象和原型对象

- **实例的属性需要显性地定义在this对象上，否则都是定义在原型对象上的**
  ```js
    class Point {
      constructor(x, y) {
        this.x = x;  // this指向实例对象
        this.y = y;
      }

      toString() {}

      toNumber(){}
    }
    var point = new Point(1, 2)

    point.hasOwnProperty('__proto__');  // false
    point.hasOwnProperty('x');  // true，实例对象上的属性
    point.hasOwnProperty('toString');  // false
  ```
  - 上面代码中，x和y是实例对象point自身的属性(this定义)，返回true
  - 但toString是定义在原型对象上的属性，所以返回 false
  - `point.__proto__.hasOwnProperty('toString')`为true，是原型对象上的属性


## 题外话

题外话，由此也可以看出
- `Object.keys()`方法返回由指定对象的属性名(不包括可枚举属性)组成的数组。
- `Object.getOwnPropertyNames(obj)`方法返回指定对象的属性名(包括可枚举属性)组成的数组。
- `obj.hasOwnProperty(prop)`方法判断对象自身属性中是否有指定的属性，不包括从原型链上继承到的属性
- `for...in...`循环只会遍历可枚举属性，包括从原型链上继承到的属性

遍历object的key
  ```js
    for (var key in obj) {
      if (obj.hasOwnProperty(key)) {
        // do something
      }
    }
  ```
  相当于
  ```js
    Object.keys(obj).forEach(key => {
      // do something
    }
  ```

  但第二种方法的性能比第一种要差些，第二种新建了一个函数的作用域

  为什么要加`hasOwnProperty`判断呢
  ```js
    class Point {
      constructor(x, y) {
        this.x = x;  // this指向实例对象
        this.y = y;
      }

      toString() {}

      toNumber(){}
    }

    Point.prototype = {foo: 'bar'}

    var point = new Point(1, 2)

    point.z = 3

    console.log(point);  // ["x", "y", "z"]
    console.log(Object.getOwnPropertyNames(point));  // ["x", "y", "z"]
    console.log(Object.getOwnPropertyNames(Point.prototype));  // ["constructor", "toString", "toNumber"]
  ```
  实例point有`x`、`y`、`z`和从原型链上继承的`foo`总共四个属性

  执行下面代码
  ```js
    for (var key in point) {
      if (point.hasOwnProperty(key)) {
        console.log('has:', key, point[key])
      } else {
        console.log('no:', key, point[key])
      }

    }
  ```
  打印出来的结果是：
  ```js
    has: x 1
    has: y 2
    has: z 3
    no: foo bar
  ```
  `for..in..`循环时会包括从原型链上继承的属性，`foo`就是从原型链上继承的属性。使用`hasOwnProperty`可以分离出对象自身的属性和继承的属性

  再次执行：
  ```js
    point.foo = 'new bar'
  ```
  打印出来的结果是：
  ```js
    has: x 1
    has: y 2
    has: z 3
    has: foo new bar
  ```
  修改对象继承的属性值时，会让继承的属性直接成为自身的属性


## 类的所有实例共享一个原型对象

```js
var p1 = new Point(2,3);
var p2 = new Point(3,2);

p1.__proto__ === p2.__proto__
```
- 这也意味着，可以通过实例的`__proto__`属性为类添加方法

- 这导致修改一个实例的原型对象时，会改写类的原始定义，影响这个类的所有实例
  ```js
  p1.__proto__.toNiu = function () {
    return 'niu'
  }
  p1.toNiu()  // 'niu'
  p2.toNiu()  // 'niu'
  ```


## 参考文档

- [class](http://es6.ruanyifeng.com/#docs/class)
- [Object.keys()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)
- [Object.getOwnpropertyNames()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyNames)
- [for..in and hasOwnProperty [duplicate]](https://stackoverflow.com/questions/12735778/for-in-and-hasownproperty/12735977#12735977)

