---
title: 解决hexo引用网络图片显示错误的问题
date: 2019-08-24 14:10:00
tags: 博客
categories: hexo
keywords: hexo引用网络的图片
copyright: true
---
## 问题
博文在本地写好，打开 localhost::4000 显示还是好的，hexo d 之后还能显示，但是过几天显示不了如图：  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/43C1F25F2921419C966D7331009D1770/10179)  
<!-- more -->
## 解决方法
打开 ``myblog/themes/next/layout/_partials`` 文件夹下的 ``head.swig`` 添加如下的代码：  
``<meta name="referrer" content="no-referrer">``