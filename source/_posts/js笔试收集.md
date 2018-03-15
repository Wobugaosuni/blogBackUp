---
title: js笔试收集
date: 2018-03-05 14:26:25
tags:
  - JS
  - 持续更新
---

## 关于setTimeout、Promise.then和常规的js的执行顺序

如题，下面代码的执行顺序是？
```js
  console.log(1)

  setTimeout(() => {
    console.log(2)
  }, 0)

  new Promise(resolve => {
    console.log(3);
    resolve()
  }).then(() => console.log(4))
    .then(() => console.log(5))

  console.log(6)
```
<!-- more -->
答案是：1 3 6 4 5 2

- 虽然`setTimeout`设置了立马执行，但在不同浏览器中，它是有延时的。chrome延时4ms，旧的ie延时1/60s。是一个异步执行的函数，在以上代码中最后执行

- `Promise.then()`也是一个异步的函数，但跟`setTimeout`相比，`Promise.then()`是一个`micro task`，`setTimeout`是一个`normal task`，`Promise.then()`远比`setTimeout`执行的快

- `Promise.resolve()`是同步的，按顺序执行

- `Promise.resolve().then(() => {})`相当于`new Promise(resolve => resolve()).then()`


再来看两个例子
```js
  setTimeout(() => console.log(1), 0)
  setTimeout(() => console.log(2), 1)
  // 1 2
```
```js
  setTimeout(() => console.log(1), 1)
  setTimeout(() => console.log(2), 0)
  // 1 2
```
上面的代码分别设置了延时0ms 和 1ms执行，但由于少于4ms，就按照4ms(浏览器最少时间)正常顺序运行
