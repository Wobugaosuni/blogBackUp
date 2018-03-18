---
title: javaScript实现大数相加
date: 2018-02-01 20:54:49
tags:
  - js
---


## 超大的数

看看此例子🌰
```js
// 例子一
9007199254740992 === 9007199254740993   // true

// 例子二
21111111111111111111111111 === 21111111111111111111111000  // true
```
按照正常逻辑，例子一和二的输出结果应该是 `false` 的，但控制台却输出 `true`

<!-- more -->

## 为何不能直接相加呢

- 如下图所示，js采用IEEE754标准中的浮点数算法来表述数字Number.
- ** js只能精确到个位的最大整数是`Math.pow(2, 53); // 9007199254740992`（就是2的53次方, 16位数） **
- 对于超出2的53次方的数字，js是怎么处理的呢？—— **丢弃超出2的53次方的数字后的位数，导致精度丢失 **

<div style="width: 600px">
  {% asset_img big-number.png %}
</div>

## github的开源

实现大数相加的功能，已经有一些开源的库了
不过基于求知欲(面试可能出现)，还是自己实现下好
- [bignumber.js](https://github.com/MikeMcl/bignumber.js)

## 实现

>  思路，如图所示，按小时候的计算方式，从右边往左边开始相加
  1. 将字符串拆分成单个元素的数组，把元素颠倒过来
  2. 从前往后，同一index的元素相加，转成字符串，再拆分成数组
  3. 将相加的结果的最后一位放进结果数组里
  4. 如果还有元素(进位)，放到下一轮相加
  5. 循环完成了。结果都在数组里
  6. 反转数组元素，合并
  7. 还要匹配第一位是0的，去掉

<div style="width: 600px">
  {% asset_img example.jpeg %}
</div>

```js
  function add(string1, string2) {
    function add(string1, string2) {
    // 实现该函数
    // 先判断，如果小于16位，直接相加
    if (string1.length < 16 && string2.length <16) {
      return ((+string1) + (+string2)).toString()
    }

    /**
    * 方法一，不能实现大数相加
    */
    // return (Number(string1) + Number(string2)).toString()
    // 大数相加
    let list1 = string1.split('').reverse()   // 将字符串拆分成单个元素的数组，把元素颠倒过来
    let list2 = string2.split('').reverse()
    let resultList = []  // 存放相加好的个位数的list
    let carry = 0  // 进位
    const cycleNumbers = Math.max.apply(Math, [string1.length, string2.length])  // 相加的次数

    let i = 0
    while (i <= cycleNumbers) {
      unitTotalList = (Number(list1.shift() || '0')  + Number(list2.shift() || '0') + carry).toString().split('')  // 个位数相加
      resultList.push(unitTotalList.pop());  // 把结果放进list里

      carry = Number(unitTotalList.pop() || '0')  // 进位的数字。默认0
      // console.log('carry:', carry)

      i++
    }
    // console.log("resultList:", resultList);

    return resultList.reverse().join('').replace(/^0/gi, '')  // 把list颠倒过来，合并。如果最大的个位数是0，丢弃

    /**
    * other
    */
  }

  module.exports = add

```

## 文档参考

- [js实现大数相加](http://www.plqblog.com/views/article.php?id=29)
