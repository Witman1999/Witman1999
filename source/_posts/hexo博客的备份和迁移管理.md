---
title: hexo博客的备份和迁移管理
date: 2019-08-30 12:10:00
tags: 博客
categories: hexo
image: 
sticky: 
keywords: hexo博客备份,利用git备份博客
copyright: true
---
# 前言
我们都知道，我们刚开始的博客比如hexo，是编译后上去的静态网页文件。我们的文章啊等等都在本地，但是如果我们换了电脑怎么办，放在U盘复制过去也不是不行。但是如果电脑死机等不定因素不能复制等，不得凉凉了。这个时候我们可以借用 GitHub 来备份源文件了。  
我们知道 GitHub 是能建立分支的。所以我们利用它在我们的博客仓库建立一个分支来保存源文件。
<!-- more -->
# 正文
## 建立一个中转站
{% note default %}
我们先建立一个文件夹，名字随便，我这里叫hexo，在这里启动 GitBash ,先克隆我们的仓库
{% endnote %}
`` git clone https://github.com/Witman1999/Witman1999.github.io.git
``  
之后就复制了我们仓库编译后的静态网页文件。
{% note info %}
这里其实是为了获得版本管理的 **.git** 
{% endnote %}  
## 建立分支
这里建立分支,我这里分支名为 hexo ，输入代码
``git checkout -b hexo``  
之后就建立了一个 hexo 分支
## 清空 hexo 分支
{% note default %}
这里我们都知道，我们这里只要保存源文件，不需要那些编译后的静态网页。所以要清空。
{% endnote %}
我们删除除了 .git 文件夹之外的文件或文件夹。在删除后通过代码 ``git status`` 查看到  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/E076359A39904E469777FA315D666F59/10722)  
然后保存到带添加列表：  ``git add --all``  ,这里是代表添加了所有，后面提交到本地仓库``git commit -m "清空hexo分支仓库"``，-m 后面的提交信息可以自定义。最后我们推送到远端更新``git push --set-upstream origin hexo ``  
{% note info %}
这里同时设置了以后默认为hexo分支，回到博客的根目录下就能看到。
{% endnote %}  
![image](https://note.youdao.com/yws/public/resource/359e08a52f64deaac553adb0132327ad/xmlnote/01059B3791674B998D870508B8FB8397/10765)  
{% note info %}
后面红线标注的就是当前的分支。
{% endnote %}  
{% note warning %}
查看文件，这里我们的博客的站点配置文件 _config.yml 的默认提交分支要确保为 master 
{% endnote %}  
```html
deploy:
  type: git
  repo: https://github.com/Witman1999/Witman1999.github.io.git
  branch: master #提交的默认分支
```
## 移动文件
把 .git 文件夹移动到博客的根目录下
## 提交源文件
{% note warning %}这里的主题文件，在 themes/ 文件夹下，有些是克隆 Github 下来的，有着 Github 的 .git版本管理文件，这里要删除 .git文件夹和 .gitignore 文件，不然会忽略这个 next 主题{% endnote %}  
然后安装更新 Github 的仓库的步骤，在博客的根目录下，输入  
1. ``git add --all``
2. ``git commit -m`` "提交源文件"
3. ``git push`` （这里要确保提交的分支为 hexo ，在前面的步骤可以查看，如果不是可以输入 ``git checkout hexo``切换分支）

