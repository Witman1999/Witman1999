---
title: fatal unable to auto-detect email address (got 15153@DESKTOP.(none))的解决方法
date: 2019-10-17 13:10:00
tags: GitHub
categories: Git Bash
keywords: 
copyright: true
---
### 问题
使用``git commit -m "......" `` 提交的时候，报出了下面的问题  
*** Please tell me who you are.  
```   
Run  
  
  git config --global user.email "you@example.com"  
  git config --global user.name "Your Name"  
  
to set your account's default identity.
Omit --global to set the identity only in this repository.  

fatal: unable to auto-detect email address (got '15153@DESKTOP-0U0U3NE.(none)') 
```

<!--more-->
### 解决方法
找到工程目录的 ``.git`` 文件夹，打开之后找到````config`` 文件，在最后边添加如下信息：
```
[user]
email=your email
name=your name
```
#### 注意
这里 ``.git`` 为隐藏文件，并且 ``your email`` 和 ``yourname`` 这里对应你的要修改的。

