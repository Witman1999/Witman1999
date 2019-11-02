---
title: centos 6 mini虚拟机安装教程
date: 2019-10-27 10:10:00
tags: Vmware
categories: Linux
copyright: true
---

# 配置安装环境
**打开 ``Vmware Workstation`` 虚拟机，点击“创建新的虚拟机“** 
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/1BE1DADD20B849BFA35C81B57F036979/13474)
  
 <!--more-->
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/40E0BAC1F93B42EEA840C4D0518FEF84/13476)  

**在这里，我选择自定义来设置更多的内容，然后选择下一步**  

![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/454CF51E963F4E5DA9B231F1D41B5024/13491)  

**选择稍后安装操作系统**  


![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/43F674B677754591B69F88771205A230/13497)  

**这里选择 linux ，下面系统选择 CentOS6 64位（这里是根据自己所下载的系统的位数和系统的版本来决定）**  

![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/16D3191BBE29494B9EC4C7102609483C/13504)  

**选择虚拟机创建后的保存位置，可以设置为默认（建议更改到其他盘，路径尽量不要有中文）。**  

![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/52AAC38F8D814A5F89874D01E7BA55D4/13508)  

**这里的 CPU 数，根据自己电脑情况来分配。**  

![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/A4AA7FCACA7C4ED2B319F4CA96195076/13512) 
 
**内存大的例如 8 G ，可以3~4G，然后点击下一步**  

![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/580E1ACC65E8476FBD092387E56E256E/13522) 
 
**选择 nat 网络连接模式，下一步**  

![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/BFF1CAAADC064ECCA27A6F18DCE75E6F/13525) 
   
**选择 LSI Logic 推荐， 然后下一步**   

![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/FCAA83AD9DC84CAC880275C7CFA1F7E0/13532)  
  
**默认，下一步**  

![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/3B3F8D74D62F4FD08D91E514F5644258/13539)  

**设置磁盘的种类，我们选择创建新的虚拟磁盘。**  

![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/F018020424F943119884A3EEAF976BD0/13551)  

**设置虚拟磁盘的大小，将磁盘拆分成多个文件，以免一次性占用自己电脑的资源，节省空间**   

![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/02780268EEBE47E1A2F9EB62118490A5/13553)  

**选定存虚拟磁盘文件的位置，然后点击下一步**  
**到了这步，就基本配置完成。**  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/6D77243CCE2C4759A2A8902EFC3F25FA/13562)  

**双击 CD/DVD ，找到下载的系统的位置**
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/8BEECB8535A04679A160ED5DA59B8D1E/13564)   

--- 
# 启动虚拟机
**然后启动虚拟机，开始我们遇到这个界面，按 Esc 键**  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/4E1B7F40430644DC828E550C81E4204C/13580)  

**在这里，我们输入 linux text**  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/A1CDCBA9E5C846669696F8155D09BCAE/13573)  

**后面，这里问是否测试一下，测试要需要点时间，我们选择跳过**  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/B0806EBE2406458B95349FF91ABA441B/13590)  

**在这里，选择系统语言，因为用中文它还是自动会改为英文，那么我直接选择英文**  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/D2310BBDC05D4C4AAC897ED79B4E414B/13594)  

**这里选择键盘的方式，我的是美式选择 US**  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/15A8FEAAAE304C66A77AA7423887E205/13592)  

**这里是提醒设备需要初始化，我们就选择初始化全部**  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/5BF22BDED23945529891B1519ED20072/13589)  

**接下来这一步选择的是时区，我选择亚太地区香港**  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/53426AC3258E43B7A3292761DE7ADD18/13593)  

**到达这一步，设置 根用户（root 用户）密码：**  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/369DCE9D9556472AAC514CEA53B851F3/13599)  

**然后设置分区的种类，我们选择默认的替换已经存在的 Linux 系统，这里其实我们在虚拟机创建，Linux 也是不存在的。**   
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/D66EF69F04774D27BC3F359788DA4EB2/13591)    

**这里提醒存储设备将被修改重置 选择 Write changes to disk**    
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/ED6F51B787E541E3B1DF21670EB852E2/13597)  

**后面静静的等待安装完成就行**    
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/65B73D128E7D48D8811925B12FB68A17/13598)  

**安装成功后，提醒我们进行重启**  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/77B2C25806A54DAB838668FA0B0A979C/13595)  

**重启之后  login 我们输入 root , password 输入我们之前设置的密码， Linux 系统之下，是不显示密码。**  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/41011AD81FF5440191AE5719107FD751/13601)   

**这里我输入 cd .. 返回上一个目录，然后 ls 查看当前在那哪个目录之下，测试系统是否成功**  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/AECDD877B8874B3AA891F5FFE7DBF004/13600)  
**至此安装完成。**


