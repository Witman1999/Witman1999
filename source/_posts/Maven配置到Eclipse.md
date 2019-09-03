---
title: Maven配置到Eclipse
date: 2019-09-3 16:30:00
tags: 
categories: Maven
copyright: true
---
# 安装 maven
打开 Eclipses ，点击上方工具栏的 **windows**->**prferences**，弹出如下所示：  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/8DB06D952420423786F249B829C71A54/11061)  
<!-- more -->
双击 **maven**。     
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/1F088BA22F2247F19FA5BE82C4EE63F9/11196)  
如图所示，先点击``installations``再点击``add``。  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/17D0847F8F34417C8F8FE549FB36EA7C/11210)  
点击``directory``找到你**maven**的解压后的文件夹并且按确定，最后``finish``。  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/90647E80762E4437A08033CA614CBC61/11217)  
后面更改默认选项选中它。  
{% note info %}
这个时候安装到 Eclipse 中了。但是，我们都知道 maven 的原理就是集中管理 jar 包的工具，用到的的 jar 包都是来源于三个地方，分别是 中央仓库，本地仓库，远程仓库（私服）。这里我们要让它为了方便从本地仓库导入 jar 包，需要以下操作。
{% endnote %}
# 连接本地仓库  
## 编辑 settings.xml
找到 maven 解压后的文件夹，打开``conf``文件夹，就能找到。修改如下：  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/FE1AD4FB39E743C1A098B3A21B4FCDDC/11248)  
这里面的``D:\MyApp\maven\Maven-Repository``就是本地仓库的位置，按照自己的路径要修改它。
## 回到Eclipse
点击工具栏的 ``windows``->``prference``->``maven``  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/41C2F3DAF47F48F791A18122B131B2C7/11258)  
点击 ``user settings``，之后点击``browser``找到刚才的``settings.xml``，下面的``Local Repository``会自动显示到你设置的本地仓库。最后点击``Apply and Close``就行。  
后面就可以添加**Maven**工程了。