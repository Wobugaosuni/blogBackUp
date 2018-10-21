---
title: PC端手机适配代码检测
date: 2018-10-21 16:26:04
tags:
  - JS
---

## 场景

在开发中遇到这种场景，一个项目有两套代码，一套PC端的，一套手机端H5的。
需求场景是，当用户用PC端的地址在手机端进入时，能检测到用户是用手机端访问的，从而跳转到H5的页面。

## 方法一，使用 navigator.userAgent

`navigator`是`window`的属性之一，使用该方法就不用考虑浏览器兼容的问题了，可以大胆放心地用

<!-- more -->

- 首先复习下 `window.navigator` 浏览器属性
返回一个navigator对象的引用,可以用它来查询一些关于运行当前脚本的应用程序的相关信息.
具体的属性可以参考：https://developer.mozilla.org/zh-CN/docs/Web/API/Window/navigator

- navigator.userAgent 是 navigator 的属性之一
返回当前浏览器的用户代理（user agent）字符串。

- 例子
```js
  window.navigator.userAgent
  // "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36"
```
可以使用该方法 + 正则 来判断运行该脚本所在的设备

- 下面的方法基本是通用的用来检测设备的祖传代码了
```js
  let isMobile = false

  if (navigator.userAgent.match(/Android/i) ||
    navigator.userAgent.match(/webOS/i) ||
    navigator.userAgent.match(/iPhone/i) ||
    navigator.userAgent.match(/iPad/i) ||
    navigator.userAgent.match(/iPod/i) ||
    navigator.userAgent.match(/BlackBerry/i) ||
    navigator.userAgent.match(/Windows Phone/i)
  ) {
    isMobile = true
  }

  if (window.innerWidth <= 800 && window.innerHeight <= 600) {
    isMobile = true
  }

  if (isMobile) {
    console.log('手机ipad等设备')
  } else {
    console.log('大设备')
  }
```
如果 `navigator.userAgent` 都不顶用，再祭出 `window.innerWidth` 终极武器了

## 方法二，使用 `window.matchMedia()`方法

该方法简单易用，一句话就能判断用户所使用的设备了。但是，浏览器支持不佳，目前开发的话，fire掉

- mdn文档支持
https://developer.mozilla.org/en-US/docs/Web/API/Window/matchMedia

- 语法
  `mql = window.matchMedia(mediaQueryString)`
  改方法返回一个 `MediaQueryList`，如：
  ```js
  {
    matches: true
    media: "(min-width: 400px)"
    onchange: null
  }
  ```
  我们可以根据返回的 `matches` 属性，判断设备是否符合查询条件

- 例子
  ```js
  if (window.matchMedia("(min-width: 400px)").matches) {
    /* the viewport is at least 400 pixels wide */
  } else {
    /* the viewport is less than 400 pixels wide */
  }
  ```

- 浏览器支持情况
  <div style="width: 500px">
    {% asset_img 1.png %}
  </div>
可以看到，为什么这个方法很少开发会选择使用了。PC端的浏览器基本支持该方法。但到了手机端，安卓、谷歌等浏览器不支持。



