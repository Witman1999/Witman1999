---
title: 搭建博客（hexo）
date: 2019-08-17 14:10:00
tags: 博客
categories: hexo
image: /images/置顶.jpg
sticky: true
keywords: 搭建博客的笔记
copyright: true # 新增，开启版权说明
---
---
<!-- more -->
# 一. 下载 nodejs
点击 [node.js](https://nodejs.org/en/) 官网，就可以进行下载，例如下图：


![image](https://note.youdao.com/yws/public/resource/fde450b8e5a0062a91d41f0c1552b69d/xmlnote/3BCC50B163104CE6BE69568E28EE0FD0/9528.jpg)  
安装之后，打开终端(win+R)，输入 cmd,之后在终端输入：
```
node -v
npm -v
```

结果如图：  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/5A84A6A4214F4AD88D9B4E830D245289/9826.png)
# 二 安装 hexo
## 终端输入
```
npm install -g hexo-cli
```
## 验证
在终端输入
```
hexo -v 
```
结果如图：
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/75241645573F4D348F974DC29621F9E7/9843.png)
# 三 搭建
1. **建立一个空文件夹，名字任意（我的为 myblog）**
   - 以后出错直接将该文件夹删掉重来就行
2. **终端进入 myblog 文件夹**
3. **初始化博客，终端输入**
    - hexo init
4. **启动博客查看**
    - hexo server(按 ctrl+c 停止服务)
5. **浏览器输入**
    - localhost::4000
6. **新建文章**
    - hexo new post "我的第一篇文章"
7. **生成**
    - hexo clean（清空）
    - hexo g（配置）
    - hexo s（开启服务）
# 四. 部署到 GitHub
1. **创建个人账户**
2. **在 GitHub 创建仓库**
    - 注意：用户部署个人博客的 GitHub 仓库的命名必须和 GitHub 用户名（昵称）一样
3. **装 git 插件**
    - 终端输入： npm install -save hexo-deployer-git
4. **修改 myblog 文件夹下的 config.yml（站点配置文件）**
    - 拉到底部看到 deploy 改成
```
deploy:
    type: git
    repo: https://github.com/yourname/yourname.github.io.git
    branch: master
# 其中yourname是你 GitHub 用户名（记住，仓库名必须和 GitHub 用户名一样）
```
5. **部署远端**
    - 终端输入：hexo d
# 五 更换主题
以 nextT 主题为例子
1. **下载的主题文件放到 myblog/themes/**
2. **在 myblog 文件夹下，修改 config.yml（站点配置文件）找到如下代码**
```
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: landscape
```
**改成**
```
theme: next
```
  
   
   
---
## 参考博客
1. [Github+Hexo+NextT搭建个人博客](https://www.jianshu.com/p/57635aa8620b)
2. [Hexo框架+NextT主题搭建博客教程(部署到coding net)](https://blog.csdn.net/qq_23483671/article/details/78635372)
3. [hexo史上最全搭建教程](https://blog.csdn.net/sinat_37781304/article/details/82729029)

