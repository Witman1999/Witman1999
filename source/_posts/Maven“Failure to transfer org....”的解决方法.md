---
title: Maven基础知识
date: 2019-09-5 17:16:00
tags: 
categories: Maven
copyright: true
---
# 引言
由于第一次使用``maven``遇到了一些错误，例如标题的这个错误，详细信息是``Failure to transfer org.apache.maven.plugins:maven-compiler-plugin:jar:3.1``通过网上的查找，在这里记录下来防止下一次踩坑。
<!-- more -->
# 正文
其实这个 ERROR 是一个很平常的错误 **maven下载不完整导致的** ，只要根据错误提示找到相应的目录删除相应的文件夹，重新下载即可。
## 删除文件夹
通过提示，在我们的本地仓库下，找``org``->``apache``->``maven``->``plugins``->``maven-compiler-plugin``。  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/1AFAB6990BCC4CDCB7858EC6B201CF3B/11418)  
我的是3.1的版本有问题，可以打开看一下。    
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/CD6C086D3AE9491DBD13249C9D6D0017/11423)  
这是我的已经完整的版本，如果是没有下载完的，可能会缺少 jar 包或者少几个文件，或者有``lastUpdated``后缀名的文件，这就代表没有下载完整。可能是由于网络或者误操作没有下载完整。我这里直接整个文件夹删除掉了。  
## 重新下载
这里就简单了，打开遇到问题的项目，右键->``maven``->``Update Project``。选中要更新的工程，OK 就能自动下载了。