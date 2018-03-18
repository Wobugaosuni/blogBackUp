---
title: Hexo搭建博客 + Github pages + 域名绑定(可选)
date: 2017-09-20 19:37:32
tags:
---

## 关于Hexo
- 中文文档：https://hexo.io/zh-cn/docs/
- 是一个快速、简洁且高效的博客框架。使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页

nextT主题教程：http://theme-next.iissnan.com/getting-started.html

<!-- more -->

## 准备工作
目的：发布到个人的github网站(username.github.io)
1. 使用github pages
github pages优点：免费托管，自带主题，支持自制页面等
创建github pages，仓库名为`username.github.io`，username一定与Owner一致

2. 安装hexo
`sudo npm i hexo-cli -g`

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

## 写作
```bash
hexo new [layout] <title>
```
在命令中指定文章的布局（layout），默认为 post

## 域名绑定（可选）
**1. 买域名**
我是在[万网](https://wanwang.aliyun.com/)买的域名([annhuang.cn](http://annhuang.cn/))。域名买好之后，提交实名认证即可

**2. 域名解析，使用dnspod**
  1. 需要注册[DNSpod](https://www.dnspod.cn)
  2. 在域名解析里，选择添加域名，不用写`http://`
    <div style="width: 600px">
      {% asset_img WechatIMG213.jpeg %}
    </div>
  3. 添加域名
  4. 修改域名的dns地址为`f1g1ns1.dnspod.net`和`f1g1ns2.dnspod.net`
    - 拷贝DNSpod的记录值
      <div style="width: 600px">
        {% asset_img WechatIMG214.jpeg %}
      </div>
    - 粘贴到万网上
      <div style="width: 600px">
        {% asset_img WechatIMG215.jpeg %}
      </div>

**3. 域名与github pages进行绑定**
  具体官方文档参考：https://help.github.com/articles/setting-up-an-apex-domain/
  1. 添加CHAME记录
    其中CHAME的值为github pages的地址
    访问github.io时，重定向到annhuang.cn
    <div style="width: 600px">
      {% asset_img WechatIMG220.jpeg %}
    </div>
  2. 添加A记录
    <b>在github pages仓库上增加域名</b>
      <div style="width: 600px">
        {% asset_img WechatIMG223.jpeg %}
      </div>
    <b>添加两条A记录</b>
      <div style="width: 600px">
        {% asset_img WechatIMG222.jpeg %}
      </div>
    <b>在终端ping域名，是否成功</b>
      <div style="width: 450px">
        {% asset_img WechatIMG224.jpeg %}
      </div>
  3. 在本地站点目录里的`source`目录下添加`CHAME`文件，打开后添加域名信息`annhuang.cn`，填好之后，重新部署到github pages（hexo -g d）

**配置完成**
配置完成后，要等dns修改成功。官方说法是要一天以上才可以完成的，一般一小时左右就可以生效。
打开域名，就可以看到自己的[博客](http://annhuang.cn)

**常见问题**
每次执行`hexo d -g`命令后，打开域名会有以下报错问题"There isn't a GitHub Pages here"。原因是每次构建完，在github pages仓库上的域名都为空，需要再一次配置
<div style="width: 450px">
  {% asset_img WechatIMG225.jpeg %}
</div>

## 文档参考
极速搭建，参考：
  - http://www.jianshu.com/p/4eaddcbe4d12
  - http://www.jianshu.com/p/834d7cc0668d
