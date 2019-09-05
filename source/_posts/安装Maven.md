---
title: 安装Maven
date: 2019-09-3 15:32:00
tags: 
categories: Maven
copyright: true
---
# Maven 软件的下载
为了使用 Maven 管理工具，我们首先要到官网下载，可以百度或者点击[这里](https://www.apache.org)，官网如下：  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/E5092447F8A747418A8F52D927DADD47/11072) 
<!-- more -->  
进入里面就有``download``下载，但是在``download``页面，又有新的问题。遇到了好几个版本，分成连个类，一个是``binary``和``source``    
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/D8F0C6AA03E34F6FA083CCEBF3B9706B/11090)  
{% note info %}
通过官方的解释，大概知道，它讲的是，一个是二进制分发的存档也就是可以直接使用的，还有一个是源代码，需要自己手动编译。在这里为了方便，我就选择的 ``binary``直接安装版（手动编译会好点可能，因为能自己配置环境，能力好的可以试试）。
{% endnote %}
# 配置环境
我们把下载下来的解压包解压到一个文件夹。  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/0B73863C5FD846C7898AADA237710BC8/11114)  
右击我的电脑的``属性``   
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/BB9CD1F1C75A406D9C8B4E0CBA8F0DBC/11120)  
后面``高级系统设置``->``环境变量``->在``系统变量``的位置点击``新建``，如下图所示输入：  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/66332B263FB240448942E26C163B1CA6/11134)  
其中的变量值就是``Maven``的安装地址。之后双击``path``  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/EEDA5A9DBD3E4052A2EFFCE139C5FB99/11142)  
添加如图所示：  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/142FA141CB4549EAB3FFD263F481619B/11149)  
代码为``%MAVEN_HOME\bin%``
# 查看版本
按快捷键``win+R``输入``cmd``，然后输入代码``mvn -v``查看是否存在。  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/DF373935CFDE46DEBF77863967E3FD86/11164)  
## 注意
{% note warning %}
因为 **maven** 是用于 **java** 工程，所以要提前安装好 **java** 的开发环境（JDk）。
{% endnote %}


