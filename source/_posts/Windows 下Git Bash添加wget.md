---
title: Windows 下Git Bash配置wget
date: 2019-09-11 16:00:00
tags: 
categories: Git Bash
keywords: 
copyright: true
---
Git Bash 作为一个管理工具，在windows上可以替代cmd,但是也会缺少一些工具。
<!-- more -->
## 安装 wget
1. 下载``wget``的二进制安装包，点击[地址](https://eternallybored.org/misc/wget/)
2. 解压安装包，将 ``wget.exe`` 移动到 ``C:\Program Files\Git\mingw64\bin`` （这里其实也可以将 ``wget.exe``路径添加到环境变量中）
{% note warning %}
这里的放的路径指的是``Git Bash``安装路径，上面的只是示例，依照个人的安装路径为准。
{% endnote %}
