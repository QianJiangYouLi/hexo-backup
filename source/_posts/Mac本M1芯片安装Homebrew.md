---
title: Mac本M1芯片安装Homebrew
top_img: https://picsum.photos/seed/picsum/1920/942
cover: https://picsum.photos/seed/picsum/470/315
date: 2023-06-05 20:13:28
tags: mac
categories: 软件与工具的安装配置
toc_number:
updated:
keywords:
description:
sticky:
aplayer:
---

# 说明

之前安装的brew被折腾坏了，重新安装出现了一些问题，之前安装homebrew的方式不好用了，网上资料很多，折腾了一番，最后成功了，整理好这篇记录，避免一些坑。

# 系统版本

版本：macOS Monterey@12.5.1

芯片：Apple M1

# 安装

（1）终端输入

~~~bash
/bin/zsh -c "$(curl -fsSL https://gitee.com/huwei1024/HomebrewCN/raw/master/Homebrew.sh)"
~~~

![](https://pic.imgdb.cn/item/6314587116f2c2beb11f9e0e.jpg)

（2）选择镜像

homebrew官网提供的地址速度很慢，很大的可能会失败，这里选择的是中科大下载源，只要输入序号1就行。

![](https://pic.imgdb.cn/item/6314596316f2c2beb120ea56.jpg)

（3）终端会提示警告信息，根据需要选择备份还是直接安装

![](https://pic.imgdb.cn/item/631459db16f2c2beb1218561.jpg)

（4）输入Y

![](https://pic.imgdb.cn/item/63145a3c16f2c2beb121f926.jpg)

（5）输入密码，会正式开始安装，终端会有进度

![](https://pic.imgdb.cn/item/63145ac516f2c2beb122a9c6.jpg)

（6）完成安装

出现如下提示，说明已经安装成功

![](https://pic.imgdb.cn/item/63145cfc16f2c2beb1268c48.jpg)

# 排坑

按理，成功安装后就可以使用了，但在终端输入`brew -v`后出现如下错误提示

![](https://pic.imgdb.cn/item/63145d9216f2c2beb1276187.jpg)

这是git的配置问题，在终端执行`git config --global core.autocrlf`，显示true，则执行`git config --global core.autocrlf input`,然后重新执行安装命令。

出现下面的提示说明安装成功：

![](https://pic.imgdb.cn/item/63146db516f2c2beb13cb348.jpg)

![](https://pic.imgdb.cn/item/63146ddc16f2c2beb13cd42f.jpg)



感谢[CunKai](https://gitee.com/cunkai/HomebrewCN.git)的开源项目，对我的帮助很大。

# 排坑2

按照上面的方式安装好brew后，在执行brew安装时会报：

![](https://pic.imgdb.cn/item/6314757016f2c2beb14440b2.jpg)

解决这个问题只需要在终端输入`brew -v`,然后执行提示中的git命令

![](https://pic.imgdb.cn/item/6314757016f2c2beb14440b2.jpg)

~~~bash
git config --global --add safe.directory /opt/homebrew/Homebrew/Library/Taps/homebrew/homebrew-core

git config --global --add safe.directory /opt/homebrew/Homebrew/Library/Taps/homebrew/homebrew-cask
~~~

安装tree测试：安装成功

![](https://pic.imgdb.cn/item/631476fb16f2c2beb145eaf9.jpg)

