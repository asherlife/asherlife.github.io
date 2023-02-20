---
title: Github+hexo新手教程
tags: 
- 原创
categories:
- 教程
---


>看到朋友搭了个个人博客发布一些读书心得，然后最近自己工作上也处于项目间隔期，个人时间比较多，就用摸鱼的时间利用[github pages](https://pages.github.com) + [hexo](https://hexo.io/zh-cn)简单搭了一个博客。下面就用一些篇幅来描述一些搭建过程中遇到的问题和踩过的坑，当然也有具体步骤。


# 具体搭建步骤


查阅了诸多博主的博客，思路变得清晰：简单易上手又想免费。所以选择的搭建框架也是极其普罗大众的，但确实又能满足新手小白的好奇，以及增添点职场菜鸟的自信心，话不多说，上路。


## 一、环境准备


因为本菜鸟首先预见到自己会在多个PC端维护自个的个人博客，所以会想到的就是在多个PC如何同步的问题（云同步是不可能云同步的，太没有技术难度了），但考虑的还是太晚了，博客已经大致成型了，才想到把本地source文件夹（你的博客源代码）同步，因为很多博主其实在搭建过程中是没介绍把博客源代码备份的，结果绕了一大圈（变相让自个熟练了一把git），最终还是完成了搭建。现在只需要1.hexo s（本地预览）2.hexo g -d（部署到github.io）3.git commit/push（备份博客）即可。
接下来！！！开始


### 1. 基本环境

这里不多做介绍，因为工作电脑是环境是完备的（git&&node.js），其次，这也简单，我在自己配置低下的个人电脑上确实也再次安装了一遍。你只要能找到人家的官网下载就成。

[git](https://git-scm.com/downloads)

[node.js](https://nodejs.org/en/)

[github](https://github.com/)

### 2. 安装hexo

执行安装：`npm install -g hexo-cli`

查看版本：`hexo -v`

**到这里hexo环境就初步安装好了，接下来就是创建博客，<s>更多的博客编写和个性化配置后面的部分再细说</s>**

初始化自己的博客：`hexo init 自己的博客名`

进入创建的文件夹之后执行：`npm install`安装依赖，接下来就可以执行`hexo g`，`hexo s`在本地`https://localhost:4000`查看默认的博客

### 3. 预备github pages

这个部分是简单的，就看你对github熟不熟悉，新建一个自己的`repository`，唯一需要注意的就是在命名的时候需要把Repository name改为`github用户名.github.io`的形式，不用问，问就是这就是你的个人博客网页地址。

再有就是你新建好了之后，在repository的settings-Code and automation-pages没有那么快发布，要等待一会，网页才会发布成功。

## 二、发布到github pages，并设置同步

发布文章以及主题设置的部分，在网路上（我为什么要用港台那边的说法？？？）有非常多的设置，个人很享受一点点摸索配置的过程，没有技术难度，但是把自己的个人信息post一点点放进网页的过程还是快乐的，所以这一部分不会多说，最主要楼主不愿意多花时间哈哈哈哈。

### 1. 部署到github pages

在预备github pages的过程中，你的个人博客网站其实已经完成了，你在repository的code中新建一个HTML或者markdown文件就可以预览到效果，那么如何将我们在hexo本地写的.md文件初始化成的静态网页部署到github pages上呢。

一般有两种方式，一个简单粗暴，把你的public文件直接推送到repository某分支中，后期编写完博客.md文件，生成并预览无误之后也是直接git push。

这里介绍另外一种，因为在同步的时候也需要push到指定分支，所以难免会忘记一个，但是如果两个操作不同，就可以形成流水线，不怎么会忘。

安装hexo-deployer-git：`npm install hexo-deployer-git --save`

修改hexo根目录_config.yml文件的deploy配置

    deploy:
        type: git
        repo: repository地址.git
        branch: main
        token: GitHub 的 Personal access tokens

好的！现在！就是现在！见证奇迹的时刻！

`hexo g -d`：就可以实现本地编写的博客部署到`https://用户名.github.io`

### 2. 同步自己的博客文件夹

这块有很多的教程，主要就是涉及github和git操作，以及个人偏好。


- 备份习惯（你的习惯直接整个文件夹同步到云端，还是习惯于写完代码git push到repository）

这里主要介绍俺的做法，综合了许多博主的做法以及操作难度，当然还有硬要push到repository的执念。

- 首先初始化本地blog文件夹，就是你hexo init 的那个：`git init`
  - 这里你可以添加.gitignaore文件忽略不用备份的文件，除了自带的一些忽略，还可以添加.history，hexo产生的history文件太多了
- 接着就是关联本地库到远程库：`git remote add origin 仓库地址.git`
  - 也就是https://github.com/用户名/用户名.github.io.git
- 然后就是将本地文件推送到仓库指定分支（在这里我是推送到`用户名.github.io`里的master分支
  - 常规操作：`git add .`、`git commit -m '注释'`、`git push origin master`或`git push -u origin master`
  - 然后也是小技巧，把repository的默认分支从main（public文件提交分支）改为master（文件备份分支）
- 最后就是在新设备上的拉取操作了！！！


## 三、个性化

正如前面所说，不准备对这个部分进行详述，因为教程多 + 需求不一，就有博主说不喜欢Next，所以就更新了fluid的配置；另外诸如添加评论、流量量的配置属于锦上添花型的，也因人而异可有可无。

楼主所用的配置是入门式的，后面有时间或者闲的时候会继续摸索。
- 主题配置：[fluid](https://fluid-dev.github.io/hexo-fluid-docs/guide/)
- 记录网站评论和浏览量：[Leancloud](https://www.leancloud.cn/)

## 四、坑

### 1. 操作不熟练的问题

实际操作过程中真实遇到的坑实际上不多，多数是对git以及github的不熟悉，多搜索，不是提倡那什么搜商嘛，多搜搜，大不了错了再来

### 2. 真坑

- 第一个就是博客同步的问题，因为刚建博客查看教程的时候确实没考虑到备份以及多端同步的问题，所以后期再考虑多少有点晚，但事实上也就还好，IDE傻瓜化的git操作让命令行变得很生疏。
  
- 第二个是真坑。为什么说是真坑呢，因为是leancloud版本的问题。
  
  - 大多数遇到的是使用国际版的原因，而我使用的是国内版，也遇到了配置url的问题，若不配置，启用浏览量是无作用的（亲测无用）。可能是教程过于遥远的原因把
  
        修改serverURLs: https://xxxxxxxx.api.lncldglobal.com
        修改server_url：https://xxxxxxxx.lc-cn-n1-shared.com
        其中xxxxxxxx是leancloud中应用凭证的服务器地址、


## 五、后记

第一次尝试记录，后面可能会更新博文，毕竟是作为一个表达能力没那么好的人。

## 六、To do

摸索界面配置
评论失效bug解决










