---
title: 关于table
date: 2017-09-20 16:09:43
tags: CSS
---

## 单元格固定的宽
表格table下td设置单行文本超出隐藏后，单元的宽还是由单元元内容宽决定，如想要固定的宽，需要设置成：
```
table {
  table-layout: fixed;
}
```
例子：
run in jsbin: https://jsbin.com/cewajokayu/edit?html,css,output


## 单元格固定的高（单元格固定的高）
#### 使用场景
进行页面缩放时，尤其比例较大时，虽然已经对单元格的高设置了高度，但看元素时，仍然可以看出，单元格的高增加了。如图所示

<img src="./table.jpeg" width="650" />


但旁边的参照物，div元素的高是没有增加的

如果想把tr的高度固定，可以采用以下方法

#### 固定高
思路：在td里面嵌一层div，给div一个高
run in jsbin: https://jsbin.com/judabiyise/edit?html,css,output

#### 文档参考
- https://stackoverflow.com/questions/2092696/how-to-fix-height-of-tr
