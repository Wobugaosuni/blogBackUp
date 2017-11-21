---
title: 前端用的小技巧(JS，Util)
date: 2017-09-18 20:06:38
tags:
  - JS
  - Util
  - 持续更新
---

在业务开发中，会遇到很多交互相关的小细节，涉及到js的，都可以写在util里，作为一个小工具使用

<br />
## 计算字符串的物理长度(px)
- 使用场景
当不确定字符长度，又需要给元素一个相对的宽度时，应该怎么做呢？
  - 第一时间考虑的可能是给一个`百分比`。字符超过这个长度时，可以让超出的字符用'...'显示。但字符都很短时，宽度就撑不开了
  - 第二种方法是，使用 `string.length` 计算字符的长度。但一个问题是，汉子和英语的字体宽是不一样的，甚至每个字母的宽都可能不一样
  - 第三种方法，是我目前觉得是第一选择的方法。计算已经渲染后的字符串的物理长度

<!-- more -->
<br />
- 实现的函数
  ```js
  /**
   * 计算字符的长度
   * @param {*} text
   */
  export function getTextWidth(text) {  // 参数为单个字符串
    const canvas = document.createElement('canvas') // 新增 canvas 元素
    const context = canvas.getContext('2d') // 返回 canvas 的上下文绘图环境
    const metrics = context.measureText(text)  // 测量字符串的宽
    return Math.ceil(metrics.width)  // 向上取整
  }
  ```

<br />
<br />
## 获取数组里重复的值的index
- 使用场景
做递归循环的输入或者选择组件时，一般不允许用户输入或选择重复的值。对于交互，可以把重复的值凸显出来。这时候关键的点是，如何获得重复的值呢？
  1. 把递归的值放到数组里
  2. 获取重复的index，放到一个新数组里

<br />
- 实现的函数
  ```js
  /**
   * 获取数组里重复的值的index
   * return array
   */
  export function getDuplicatesIndexList(array) {
    const duplicates = {} // 把数组元素作为对象的属性，如果已经有了该属性，说明这是数组里重复的元素
    const indexList = []

    for (let i = 0; i < array.length; i += 1) {
      if (duplicates.hasOwnProperty(array[i])) {
        // 重复的(不包括第一个)
        indexList.push(i)
      } else if (array.lastIndexOf(array[i]) !== i) {
        duplicates[array[i]] = ''
        // 是否加入第一个重复的值
        // indexList.push(i)
      }
    }

    return indexList
  }
  ```

<br />
<br />
## 随机生成id
使用场景
mock数据时，经常出现产品id，要求有唯一性的。有两种方法：
  1. 手动输入id，如`productId: 101`等等。但存在大量数据时，就会有一个问题，维护非常麻烦！
  2. √ 利用`Math.random`随机生成，转成字符串(`num.toString()`)后，使用`string.slice(num)`进行裁剪:
    ```js
    Math.random().toString().slice(2)
    ```

<br />
<br />
## 类型转换函数，将字符串转为数字
  ```js
  function type (d) {
    d = +d; // "+": 将字符串转为数字，并覆盖原来的值
    return d;
  }
  ```

<br />
<br />
## JSON深拷贝
  ```js
  function deepClone(json) {
    return JSON.parse(JSON.stringify(json))
  }

  var a = {
    a: 1,
    b: { c: 1, d: 2 }
  }
  console.log('deepClone a is:', deepClone(a))  // deepClone a is: {a: 1, b: {…}}
  ```

<br />
<br />
## 获取数组的最大值和最小值
  ```js
  function maxInList(list) {
    return Math.max.apply(Math, list)
  }

  function minInList(list) {
    return Math.min.apply(Math, list)
  }

  var list = [5, 458 , 120 , -215 , 228 , 400 , 122205, -85411]
  console.log('max number is:', maxInList(list))  // max number is: 122205
  console.log('min number is:', minInList(list))  // min number is: -85411
  ```
