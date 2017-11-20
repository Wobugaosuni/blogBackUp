---
title: CSS小技巧
date: 2017-11-17 18:02:50
tags:
  - CSS
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
