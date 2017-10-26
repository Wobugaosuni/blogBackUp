---
title: JS精炼
date: 2017-10-26 14:57:01
tags:
  - JS
---

<br />
## not defined 和 undefined区别
虽然英语语义上都是“尚未定义”的意思，但在代码运行时，他们之间的语境是不同的

<!-- more -->

<br />
**not defined**
未定义，未声明的
demo:
```js
console.log(a);   // Uncaught ReferenceError: a is not defined
```

<br />
**undefined**
定义了，但没有赋初始值
定义了不赋值的作用：执行时不会报错的无意义的代码
demo:
```js
var a;
console.log(a);  // undefined
console.log(b);  // undefined
var b;  // 变量提升
```

<br />
**参考**
http://www.jianshu.com/p/eca505f12095
https://stackoverflow.com/questions/24502643/javascript-variable-undefined-vs-not-defined
