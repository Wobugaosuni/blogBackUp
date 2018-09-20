---
title: webpack的日常使用技巧
date: 2018-09-20 15:09:44
tags:
  - webpack
---

## 神奇的 chunkhash

- 使用场景
打包出来的文件，不加chunkhash或者hash。会有缓存的问题，需要手动的去清缓存，比较麻烦

一般这样写：
`chunkFilename: '[name].js',`

- chunkhash
会比较某个文件的改动历史，如果没改动，chunkhash不变。如果改动了，chunkhush会变化。这既保证了有用的缓存，对于改动的文件也立马反应到页面上

<!-- more -->

使用：
`chunkFilename: '[name].[chunkhash:8].js',`

- hash
类似于时间戳，无论文件是否有改动，hash都会变化

使用：
`chunkFilename: '[name].[hash].js',`

- 参考
  - 官网：https://webpack.js.org/configuration/
  - 博客：https://zhuanlan.zhihu.com/p/23595975


## plugins

- CommonsChunkPlugin

在多页应用里，经常会引进一些共用的部分，例如头部、侧边栏等。这时候打包时，就需要从多个模块中提取共用的模块了。可以使用 webpack 的插件 `CommonsChunkPlugin`。

配置文档是：[CommonsChunkPlugin](https://webpack.js.org/plugins/commons-chunk-plugin/#passing-the-minchunks-property-a-function)

```js
  plugins: [
    // 从多个模块中提取共用的模块到common.js
    new webpack.optimize.CommonsChunkPlugin({
      name: 'common',
      filename: 'common.js',
      minChunks: 2,
    }),
  ],
```

相应的配置项解析：
```js
{
  name: string,
  names: string[],
  // 这是 common chunk 的名称。已经存在的 chunk 可以通过传入一个已存在的 chunk 名称而被选择。
  // 如果一个字符串数组被传入，这相当于插件针对每个 chunk 名被多次调用
  // 如果该选项被忽略，同时 `options.async` 或者 `options.children` 被设置，所有的 chunk 都会被使用，否则 `options.filename` 会用于作为 chunk 名。

  filename: string,
  // common chunk 的文件名模板。可以包含与 `output.filename` 相同的占位符。
  // 如果被忽略，原本的文件名不会被修改(通常是 `output.filename` 或者 `output.chunkFilename`)

  minChunks: number|Infinity|function(module, count) -> boolean,
  // 在传入  公共chunk(commons chunk) 之前所需要包含的最少数量的 chunks 。
  // 数量必须大于等于2，或者少于等于 chunks的数量
  // 传入 `Infinity` 会马上生成 公共chunk，但里面没有模块。
  // 你可以传入一个 `function` ，以添加定制的逻辑（默认是 chunk 的数量）

  chunks: string[],
  // 通过 chunk name 去选择 chunks 的来源。chunk 必须是  公共chunk 的子模块。
  // 如果被忽略，所有的，所有的 入口chunk (entry chunk) 都会被选择。

  children: boolean,
  // 如果设置为 `true`，所有  公共chunk 的子模块都会被选择

  async: boolean|string,
  // 如果设置为 `true`，一个异步的  公共chunk 会作为 `options.name` 的子模块，和 `options.chunks` 的兄弟模块被创建。
  // 它会与 `options.chunks` 并行被加载。可以通过提供想要的字符串，而不是 `true` 来对输出的文件进行更换名称。

  minSize: number,
  // 在 公共chunk 被创建立之前，所有 公共模块 (common module) 的最少大小。
}
```

- ExtractTextPlugin

将模块里共用的模块抽取出来后，需要进一步地分离 js 和 css 代码。所用到的插件是 `ExtractTextPlugin`

配置文档是：[ExtractTextPlugin](https://webpack.js.org/plugins/extract-text-webpack-plugin/#options)

```js
  // 分离 css 和 js 文件
  new ExtractTextPlugin({
    filename: '[name].css',
    allChunks: true,
  }),
```

需要注意的一点是，当使用 `CommonsChunkPlugin` 并且在公共 `chunk` 中有提取的 `chunk`（来自`ExtractTextPlugin.extract`）时，`allChunks` 必须设置为 `true`


