---
title: 前端用的小技巧(JS)
date: 2017-09-18 20:06:38
tags: JS
---

## 计算字符串的物理长度(px)
- 使用场景
当不确定字符长度，又需要给它一个相对的宽度时，应该怎么做呢？
  - 第一时间考虑的可能是给一个`百分比`。字符超过这个长度时，可以让超出的字符用'...'显示。但字符都很短时，宽度就撑不开了
  - 第二种方法是，使用 `string.length` 计算字符的长度。但一个问题是，汉子和英语的字体宽是不一样的，甚至每个字母的宽都可能不一样
  - 第三种方法，是我目前觉得是第一选择的方法。计算已经渲染后的字符串的物理长度

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
