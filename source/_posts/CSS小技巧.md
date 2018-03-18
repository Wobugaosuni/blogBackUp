---
title: CSS小技巧
date: 2017-11-17 18:02:50
tags:
  - CSS
  - 持续更新
---

## 关于单行文本超出宽度省略

- 固定宽度的超出省略(px)
```
white-space: nowrap; /* 不换行 */
overflow: hidden; /* 溢出隐藏 */
text-overflow: ellipsis; /* 用省略号代表被修剪得文本 */
```

<!-- more -->
- 动态宽度的超出省略(%)
当父元素的宽度是动态的百分比时，就需要用到此方法了
```css
/*
<div class="father-element">
  <div class="truncate">
    Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt
    ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco
    laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in
    voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat
    non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
  </div>
</div>
*/
.father-element {
  display: table;
  table-layout: fixed;
  width: 100%;
}
.truncate {
  display: table-cell;
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow: hidden;
}
```

## 鼠标悬浮提示文字

需求：鼠标经过时有文字注释
效果如图：
<div style="width: 250px">
  {% asset_img hover.gif %}
</div>

有两种实现方式
具体效果可查看：https://jsbin.com/diniceloze/edit?html,css,output
- 方法1，使用元素的title属性
优点：简单易用，只需给元素增加一个title属性即可
缺点：样式固定，无法个性化
例子：
  ```html
  <div title="hello world">hello world</div>
  ```

- 方法2，利用css的`content:attr()`属性抓取资料
优点：可定制化hover时的样式
例子：
  ```styl
  /*
    <div data-msg="hello son" class="method-two">hello son</div>
  */

  .method-two
    position relative

  .method-two:hover:after
    content attr(data-msg)
    position absolute
    top 20px
    left 0
    font-size 12px
    color grey
    border 1px solid grey
    padding 2px 4px
  ```
