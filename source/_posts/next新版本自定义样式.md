---
title: next新版本自定义样式（hexo）
date: 2019-08-28 16:50:00
tags: 博客
categories: hexo
keywords: next自定义样式,next 7.0 样式
copyright: true 
---
更新到最新版的 next主题我们发现自定义的 css 样式位置发生了改变。  
<!-- more -->
## 第一步
打开主题配置文件  
```
custom_file_path:
  # head: source/_data/head.swig
  #header: source/_data/header.swig
  #sidebar: source/_data/sidebar.swig
  #postMeta: source/_data/post-meta.swig
  #postBodyEnd: source/_data/post-body-end.swig
  #footer: source/_data/footer.swig
  #bodyEnd: source/_data/body-end.swig
  #variable: source/_data/variables.styl
  #mixin: source/_data/mixins.styl
  #style: source/_data/custom.styl
```
发现了这段代码，我们把``style: source/_data/custom.styl``取消注释
## 第二部
在博客的根目录下创建文件,路径为
``myblog/source/_data/custom.styl``  
这里其实发现只要和主题配置文件的路径一致就行，文件名可以自己更改。然后在里面就可以写自定义样式了。