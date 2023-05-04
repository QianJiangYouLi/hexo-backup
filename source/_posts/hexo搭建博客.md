---
title: hexo搭建博客
top_img: https://picsum.photos/seed/picsum/1920/942
cover: https://picsum.photos/seed/picsum/470/315
date: 2023-04-30 08:07:03
tags: 博客
categories: 博客
toc_number:
updated:
keywords: Hexo 博客
description:
sticky:
aplayer:
---

## 准备

>本地系统环境：Ubuntu 20.04.5 LTS
>
>Node版本：18.15
>
>Git版本：2.25.1
>
>一个github账号


系统环境不同，根据自己的系统来操作就行，步骤差不多。

Node、Git的版本选择长期稳定支持的新版本就行。

云服务器和域名不是必须的，只是为了私有化更强。

相信看到这篇文章的大部分应该对这些东西都有基本的了解，准备性的东西就不罗嗦了。

安装Hexo：

全局安装Hexo，终端输入命令：`sudo npm install hexo-cli -g`。

安装成功后终端输入`hexo -v`，看到版本号表示成功，本次版本`hexo-cli: 4.3.0`。

## 配置仓库

在github中新建一个仓库，名称必须是`用户名.github.io`,这是用于托管博客，方便其他人访问博客。

为了以后的文件托管方便，可以通过ssh的方式连接，不需要每次手动输入密码，不会的自行解决。

## 初始化本地博客

在电脑中新建一个文件夹，名字随意（为了不出现莫名错误，不要有特殊符号或中文），这里取名为Blog。

在Blog目录下打开终端，输入`hexo init`初始化博客项目，没有异常将会生成如下重要文件夹或文件：

```
.
├── _config.yml // 博客配置文件
├── node_modules // 项目依赖包
├── scaffolds // 文章生成模板
├── source // 文章
├── themes // 主题
```

终端输入`hexo g`进行静态部署，终端输入`hexo s`启动服务器，在浏览器中输入`localhost:4000`访问，出现hexo的默认页面表示博客搭建成功。

到此，博客搭建成功，但还不能访问，需要部署到GitHub或自己的服务器上才能实现让他人访问。

## 将Hexo部署到GitHub

用编辑器打开Blog目录找到`_config.yml `文件，找到`deploy`配置项,修改为如下内容：==英文冒号，冒号后要加一个空格==

```
deploy:
  type: 'git'
  repository: 'github仓库名'
  branch: main # 绑定的分支
```

光改配置还不够，需要安装git插件`deploy-git`，才能部署到github。

终端输入`npm install hexo-deployer-git --save`进行安装。

安装完成后，终端输入如下三条命令：

```
hexo clean #清除缓存文件和已经生成的静态文件
hexo g #生成网站静态文将到默认设置的public文件夹
hexo d #自动生成网站静态文件，并部署到指定仓库
```

>hexo s # 本地部署
>
>以上四个命令是经常用到的

至此，在浏览器中访问：`https://xxxxx.gibhub.io`就能访问博客了。

## 解析自定义域名

以腾讯云为例，进入域名控制台，进入域名解析页面，添加一条解析记录：

![](https://pic1.imgdb.cn/item/644703980d2dde5777323775.png)

打开Blog/source目录，添加`CNAME`文件，在里面填上自己的域名，不需要带www。

在Blog目录中打开终端，`hexo clean  hexo g  hexo d`三条命令执行一遍，打开GitHub如果CNAME文件出现在项目中，点击Settings——> pages——>Custom Domain 输入解析的域名，不要带www，然后浏览器输入绑定的域名，能打开博客说明成功。

>注意是在用户名.github.io的仓库中设置，不是主页设置

到此，自定义域名完成，可以通过自定义域名访问博客。

## 发布文章

发布文章可以使用两个命令新建`.md`的文件，命令可以二选一，但不支持手动新建：

```
hexo n "文章名"   # hexo new "文章名"
```

新建的文件默认在博客根目录的source/_posts中，默认会写入一些模板内容，修改模板在目录scaffolds/post中进行。

具体的设置看文档说明。

## 安装主题美化博客

Hexo主题很多，但使用方式都基本差不多，都是下载，然后应用。主题的配置涉及很多方面，具体的内容要翻主题文档。

这里以Butterfly为例：https://butterfly.js.org/posts/21cfbf15/#%E5%AE%89%E8%A3%9D

在博客根目录打开终端，输入`git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly`安装主题

也可以通过npm安装：`npm install hexo-theme-butterfly`

>个人喜欢通过npm的方式安装
>
>npm安装需要hexo5.0以上版本才支持，这种方式安装的主题在node_modules中，不在themes中。

升级方法：在主题目录下，运行 git pull

升级方法：在 根目录下，运行 npm update hexo-theme-butterfly

应用主题：修改根目录下的 _config.yml，把主题改为 `butterfly`

注意：该主题需要安装pug和stylus渲染器，安装命令：`npm install hexo-renderer-pug hexo-renderer-stylus --save`

为了方便升级，可以在根目录中创建文件`_config.butterfly.yml`，把主题目录中的`_config.yml`内容复制过去。

注意：是主题的yml不是根目录hexo的yml，仔细区分

所有有关butterfly的配置在新的`_config.butterfly.yml`中，它的优先级高于主题的优先级，并且会自动合并主题的不同配置。

改完后依次执行三件套部署本地，看是否配置成功，最终改好后再部署到服务器。

更具体的内容参考主题说明。

