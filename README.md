## 快捷键

```bash
## 启动本地4000端口的服务，在浏览器查看
hexo s

## 创建新文章
hexo new ${文章名}

## 打包部署
hexo d -g
```

## Yilia主题的目录结构

* ``source`` - Hexo加载主题资源的主目录，需要编译生成
* ``source-src`` - 源文件目录，编译到source目录
* ``layout`` - 模板目录
* ``languages`` - 语言配置目录

一般来说，如果你想修改页面的html，请到``layout``文件夹里直接修改；
如想修改css，js，请到``source-src``文件夹里，并通过后面介绍的开发步骤，编译到``source``里。

## Yilia的开发步骤

1. **安装node+npm**

2. **安装依赖**
进入主题根目录，执行 ``npm install``

3. **开发**
执行``npm run dev``
此时会用webpack打包，把文件编译到source文件里，但文件不会经过压缩

4. **发布**
执行``npm run dist``
最终确定版本，此时的编译会经过压缩。

- [文档参考](https://github.com/litten/hexo-theme-yilia/wiki/Yilia%E6%BA%90%E7%A0%81%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84%E5%8F%8A%E6%9E%84%E5%BB%BA%E9%A1%BB%E7%9F%A5)
