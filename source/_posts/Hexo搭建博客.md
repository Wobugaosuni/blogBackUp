---
title: Hexo搭建博客 + Github pages
date: 2017-09-20 19:37:32
tags:
---

<br />
## 关于Hexo
- 中文文档：https://hexo.io/zh-cn/docs/
- 是一个快速、简洁且高效的博客框架。使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页

极速搭建，参考：
- http://www.jianshu.com/p/4eaddcbe4d12
- http://www.jianshu.com/p/834d7cc0668d


nextT主题教程：
- http://theme-next.iissnan.com/getting-started.html

<!-- more -->

<br />
## 准备工作
目的：发布到个人的github网站(username.github.io)
1. 使用github pages
github pages优点：免费托管，自带主题，支持自制页面等

创建github pages，仓库名为username.github.io，username一定与Owner一致

2. 安装hexo
`sudo npm i hexo-cli -g`

<br />
## 编写
1. 创建一个名为username.github.io的文件夹（强迫症使然）
`hexo init username.github.io`

2. 更改主题
换成nextT的主题
```bash
cd username.github.io
git clone https://github.com/iissnan/hexo-theme-next themes/next
```

3. 基础配置
在根目录下_config.yml进行配置
```
title: 我的小空间  // 网站标题
author: Ann Huang  // 作者
language: zh-Hans  // 语言
theme: next  // 主题
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:  // 与git关联
  type: git
  repo: https://github.com/Wobugaosuni/wobugaosuni.github.io.git
  branch: master
```

4. 测试
在source/_posts/hello-world.md这篇文章是自带的，作为示例，可以帮助测试
```bash
# 在根目录下启动
hexo s
```
即可在浏览器中输入localhost:4000访问

<br />
## 发布
1. 安装**hexo-deployer-git**自动部署发布工具
```bash
npm i hexo-deployer-git -S
```

2. 测试没问题后，就可以生成静态网页文件发布到github pages了
```bash
hexo clean && hexo g && hexo d
```
g: generate，生成本地发布文件夹
d: deploy，部署，发布到github pages上

3. 打开网页：https://wobugaosuni.github.io/

<br />
## 写作
```bash
hexo new [layout] <title>
```
在命令中指定文章的布局（layout），默认为 post
