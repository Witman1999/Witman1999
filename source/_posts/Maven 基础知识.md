---
title: Maven基础知识
date: 2019-09-5 17:18:00
tags: 
categories: Maven
copyright: true
---
## 项目的一键构建
{% note primary %}
我们的项目，往往都有经历编译，测试，运行，打包，安装，部署等一系列过程，那什么是一键构建？  
这里指的是，项目从编译，运行，打包，安装，部署都交给 **maven** 进行管理，这个过程称为构建。  
一键构建：  
- 指的是整个构建过程，使用 **maven** 一个命令可以轻松完成整个工作。  
对于 web 工程，我们只要通过 ``mvn tomcat:run`` 就能简单运行（**maven**自带 **tomcat** 插件）。
{% endnote %}
<!-- more -->
## maven 的目录结构
{% note info %}
大概分为四个部分：核心代码部分，配置文件部分，测试代码部分，测试配置文件。
{% endnote %}  
对应的是：  
**maven** 标准目录结构：  
- ``src/main/java`` 核心代码部分
- ``src/main/resources`` 配置文件部分  
- ``src/test/java ``，目录放置测试代码
- ``src/test/resources`` 测试配置文件
- ``src/main/webapp`` 页面资源，js,css,图片等扽
## 常用命令
命令利用``cmd``进入该工程文件夹下运行。  
- ``mvn clean``
    - 删除编译好的项目信息（删除 targe 目录），如下图成功的示例图：  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/6AE5F83CB6064D80A8CC9941A0B0F033/11505)  
- ``mvn compile``(编译)
    - 将 ``src/main/java`` 下的代码进行编译成 ``class`` 文件输出到 ``targe `` 目录下，如下图提示成功图片：  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/13837F20481D4F7F9F1208E991F52CBE/11507)
- ``mvn test``
    - 将 ``src/main/java`` 和 ``src/test/java`` 下的代码进行编译成 ``class`` 文件输出到 ``targe`` 目录下
- ``mvn package``
    - - 将 ``src/main/java`` 和 ``src/test/java`` 下的代码进行编译成 ``class`` 文件输出到 ``targe`` 目录下，并且打包成 **war** 包或者 **jar** 包的格式（依据自己的 ``pom.xml`` 文件要求的格式）
- ``mvn install``
    - 把之前打包的**war**包或者  **jar** 包的打在本地仓库。
  
## maven 的生命周期（简介）
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/70868B0C90EC4EDBA14EED96BD7B05DC/11589)  
{% note info %}
这里其实还有一个**站点生命周期**，就先不做解释。  
而**清理生命周期**，可以用在把原先的可能在别人电脑上面移植到自己电脑上的时候，可能因为配置环境不同需要清除一次以防有问题。   
**默认生命周期**中，每个命令的构建程度不同，除了``deploy`` 需要配置一些环境，前面的命令都已经走了一遍了，也就是，单一的执行了 ``install``  也就会把之前的都执行一遍。  
{% endnote %}

