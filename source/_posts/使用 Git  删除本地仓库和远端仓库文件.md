---
title: 使用 Git 删除本地仓库和远端仓库文件
date: 2019-08-26 17:11:12
tags:
categories: Git Bash
copyright: true
---
## 使用 git bash 来删除
<!-- more -->
### 一、将文件（夹）添加到暂存区
这里假设本地和远端都有一个 test.txt 文件  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/CA04AA942D9742E5B471752E8E381E7C/10259)  
先在本地删除，通过 ·``git status`` 查看  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/12A699D9DFCF4F87808823C01996AE10/10261)  
通过`` git add test.txt`` 添加到暂存区
### 二、更新本地仓库
执行`` git commit -m "删除test.txt"`` 其中-m 后面的信息是用来说明的。  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/7B8856CD1C684E6FB026D5A73BE8C89B/10269)  
### 三、更新 GitHub 的仓库
执行 ``git push origin master ``  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/BCB2E77C531046439A8AC4C6AEF3BA5E/10275)  
之后我们查看 github 的仓库就消失了  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/E5F6FFE652ED4581ADC1F92A46E763D5/10277)  
> 其他例如更新、添加操作都类似。