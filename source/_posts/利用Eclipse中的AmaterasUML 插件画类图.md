---
title: 利用Eclipse中的AmaterasUML 插件画类图
date: 2019-10-30 16:30:00
tags: 
categories: Eclipse
copyright: true
---
如图所示，正好这几天学到设计模式，利用 **Eclipse** 来快速画出类图可以更好的理解类之间的关系   
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/EA3DD44D8950414892979A7F1116CEB1/13837)
<!--more-->
# 第一种
## 一 下载插件
[点击我](http://jaist.dl.sourceforge.jp/amateras/56447/AmaterasUML_1.3.4.zip)跳转到对应页面下载
## 二 解压缩
将下载的文件解压缩后，放在 ``eclipse`` 的安装目录下的 ``\plugins`` 的文件夹下
## 三 重启 Eclipse
重新打开后，点击 ``File -> new -> other -> 搜索AmaterasUML-> 选择class diagram -> 点击next -> 选择工程 -> 将各个类拖动到面板中进行类图生成（或者自己画）``
# 第二种
## 安装
在 ``eclipse`` 里的顶部栏，选择  ``help->install new software`` 然后输入网址（URL）``https://takezoe.github.io/amateras-update-site/ `` add 它    
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/82E65D4461C74D228F649511761EA681/13859)  
两个选项都勾上然后 next 同意协议 ，完成后重启。
## 使用
和第一步是一样的