---
title: Maven 导入 Eclipse
date: 2019-09-3 16:58:00
tags: 
categories: Maven
copyright: true
---
# 打開 eclips
点击工具栏的``file``->``import``->``maven``。  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/A50BAD957E0340CC9AF5030E172E355E/11296)  
<!--more-->
点击图中的选项，会弹出选择的窗口  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/890A1DE1C1D24F0380C816CF61813AE8/11301)  
点击``browser``之后会根据 **maven**下的``pom.xml``文件显示项目，如果有多个项目可以全选或者单选，选择需要的项目，之后点击``finish``就行。  
# 修改本地配置文件
## 乱码问题
这里可能会遇到中文乱码的情况，点击需要的项目，右击它，选择``properties``。  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/E0C3469E46D043FC91D4827DBD229A3F/11321)  
点击``resource``里面看自己修改为对应的编码格式
# 注意
{% note warning %}
第一次导入 **maven** 可能要下载 jar 包等会稍微有点长。  
{% endnote %}