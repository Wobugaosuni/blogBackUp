---
title: 关于webpack
date: 2017-09-19 16:23:04
tags:
---

## 使用场景
打包出来的文件，不加chunkhash或者hash。会有缓存的问题，需要手动的去清缓存，比较麻烦

一般这样写：
`chunkFilename: '[name].js',`

## chunkhash
会比较某个文件的改动历史，如果没改动，chunkhash不变。如果改动了，chunkhush会变化。这既保证了有用的缓存，对于改动的文件也立马反应到页面上

<!-- more -->

使用：
`chunkFilename: '[name].[chunkhash:8].js',`

## hash
类似于时间戳，无论文件是否有改动，hash都会变化

使用：
`chunkFilename: '[name].[hash].js',`

## 参考
- 官网：https://webpack.js.org/configuration/
- 博客：https://zhuanlan.zhihu.com/p/23595975
