---
title: JS精炼
date: 2017-10-26 14:57:01
tags:
  - JS
---

<br />
## is not defined 和 undefined区别
之前没注意`is not defined`和`undefined`两者之间有什么区别，都简单地理解为未定义，但代码写多了，还是发现他们两者之间有明显的区别的

虽然英语语义上都是“尚未定义”的意思，但在代码运行时，他们之间的语境是不同的

<!-- more -->

**一、not defined**
未定义，未声明的
demo:
```js
console.log(a);   // Uncaught ReferenceError: a is not defined
```

**二、undefined**
定义了，但没有赋初始值
定义了不赋值，那这个变量还有什么作用呢：`执行时不会报错的无意义的代码`
demo1:
```js
var a;
console.log(a);  // undefined
console.log(b);  // undefined
var b;  // 变量提升
```

demo2，对象的属性没有赋值的情况:
```js
var a = {};
console.log(a.b);  // undefined
```

demo3，数组的属性没有赋值的情况：
```js
var a = [];
console.log(a.b);  // undefined
```


**三、参考**
http://www.jianshu.com/p/eca505f12095
https://stackoverflow.com/questions/24502643/javascript-variable-undefined-vs-not-defined
