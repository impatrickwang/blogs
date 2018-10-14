---
title: Hello World
date: 2018-10-14
---
Hello World!

第一篇就来讲讲搭建这个博客网站的过程～

## 目标
使用[Git Pages](https://pages.github.com/)和[Hexo](https://hexo.io/)(选择Hexo的原因是因为我只看得懂js :smirk: ...)搭建个人博客网站并通过个人域名来访问。

## 步骤
1. 安装Hexo
    在安装Hexo之前先确保已经安装了NodeJs和Git，Hexo的安装详见[官方文档](https://hexo.io/docs/)
2. 初始化Hexo
    ```
        hexo init blogs
        cd blogs
        npm install
    ```
    依次调用上述三个命令，就可以创建一个本地博客网站的编写环境了。
    ```
        git init
        git add .
        git commit -m "hello world"
    ```
    调用上述三个命令利用git保存我们的改动。
3. 本地浏览
    ```
        npm install hexo-server --save
    ```
    执行以上命令安装hexo-server，然后执行`hexo server`，就可以通过`localhost:4000`来浏览博客内容啦～
4. 部署Git Pages
    首先需要在github上创建一个repository，用于存放博客的内容文件。这里简单说一下Git Pages在不同名称的repository下的区别:

    名称 | 含义 | 内容文件位置 | url
    username.github.io | 用户（机构）页面 | 文件只能存放在master分支的根目录 | username.github.io
    otherwise | 项目页面 | 文件可以存放在master分支的根目录或者根目录下的docs目录，或者gh-pages分支的根目录 | username.github.io/project-name

    我使用了blogs作为repository的名字，所以这是一个项目页面，同时我选择将内容文件存放在gh-pages分支上，并且将编辑环境保存在master分支上，这样就可以在master分支上编辑，在gh-pages分支上发布。
    这里可以先把本地的编写环境推到github上保存，下面以我的github地址为例：
    ```
        git add remote git@github.com:impatrickwang/blogs.git
        git push -u origin master
    ```
    执行上述命令后，本地的编写环境就上传到了github的master分支上。
    ```
        npm install hexo-deployer-git --save
    ```
    然后执行上面这条命令安装`hexo-deployer-it`。接下来在_config.yaml文件中添加部署的配置：
    ```
        deploy:
          type: git   
          repo: <repository url>  #git@github.com:impatrickwang/blogs.git
          branch: [branch] #gh-pages
          message: [message]  #leave this blank
    ```
    最后执行`hexo clean & hexo deploy --generate`，就完成了内容文件的发布。这个时候可以去github上看一下对应repository的gh-pages分支里就保存着博客网站的内容文件。
5. 配置github
    在repository的setting中找到关于Github Pages相关的设置，将source配置为gh-pages分支。这样就可以通过github提供的url(我这里的例子是impatrickwang.github.io/blogs)来访问博客内容了。
6. 个人域名
    这里以配置二级域名blogs.wanglihao.cn为例。首先需要在个人域名上添加一条CNAME(blogs.wanglihao.cn, impatrickwang.github.io)，将你的二级域名指向github分配给你的域名。然后在repository的配置中，配置个人域名为blogs.wanglihao.cn。
    这样就可以通过二级域名来访问博客网站了～
