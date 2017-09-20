---
title: Hexo博客配置
date: 2017-09-20 20:23:43
tags:
---

<br />
## 关于图片引用
参考文档：https://hexo.io/zh-cn/docs/asset-folders.html
- 方式一
1. 在_config.yml中，把`post_asset_folder: false`设为false。（默认是false，如果改了，要改回来。其中的一个坑，如果设为true，以下两步不生效，图片看不到）
2. 把图片放在`source/images`文件夹中
3. 通过类似于`![](/images/image.jpg)`访问图片

<!-- more -->
<br />
- 方式二
1. 在_config.yml中，把`post_asset_folder: false`设为true，打开资源文件管理功能
2. 每次通过`hexo new [layout] <title>`命令创建新文章时，自动创建一个文件夹。将所有与你的文章有关的资源放在这个关联文件夹中之后，你可以通过相对路径来引用它们
3. 引用方式：
```
# 比如，把`example.jpg`图片放在了资源文件夹中
{% asset_img example.jpg This is an example image %}
```

<br />
- 方式三
可以考虑放到cdn上，直接引用图片的线上地址，不过比较麻烦
```
![test](https://res.cloudinary.com/dhoua2kgz/image/upload/v1505728541/weilaishipAvator_cffdvb.jpg)
```

<br />
## 关于图片大小
控制图片大小的话，可以使用img标签
方式二：
hexo没有提供修改宽高的接口，可以在模板外套一层div
```html
<div style="width: 650px">
  {% asset_img table.jpeg %}
</div>
```

方式一和方式三：
```html
<img src="https://xxx.jpg" width = "150" align=center />
```

<br />
## 关于主页文章截断
本博客使用的是[yilia主题](https://github.com/litten/hexo-theme-yilia)
在主页，默认是不截断文章的（文章多长就显示多长）
但作者没有提供每一块高度设置的接口，需要手工去截断。[作者原话](https://github.com/litten/hexo-theme-yilia/issues/381)
步骤：
1. 在/themes/yilia/_config.yml配置：
```yml
# 文章太长，截断按钮文字
excerpt_link: more
# 文章卡片右下角常驻链接，不需要请设置为false
show_all_link: '展开全文'
# 数学公式
mathjax: false
# 是否在新窗口打开链接
open_in_new: true
```

2. 在文章里想要截断的位置处，增加一句：
`<!-- more -->`


