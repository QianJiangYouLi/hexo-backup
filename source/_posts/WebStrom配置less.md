---
title: WebStrom配置less
top_img: https://picsum.photos/seed/picsum/1920/942
cover: https://picsum.photos/seed/picsum/470/315
date: 2023-06-10 21:03:43
tags: WebStrom
categories: 软件与工具的安装配置
toc_number:
updated:
keywords:
description:
sticky:
aplayer:
---

## 全局安装less

前提：电脑安装了Node.js，没有安装的参考其他文章

```bash
npm install -g less
```

>注意：在mac系统或者Linux中全局安装需要在命令前加 sudo提高权限

这样安装的less是最新版的，只作为学习less用法或者不配合其他的包或者框架使用。

第三方的库或者框架使用的less版本一般都是很稳定的，不一定是最新的，使用最新的版本可能带来兼容问题，导致项目跑不起来。

安装完后，在终端输入`less --version`，出现less版本号表示安装成功。

![image-20230605205704994](https://pic.imgdb.cn/item/647ddba61ddac507cc18ac7e.webp)

## 在webstrom中配置less

（1）打开webstrom，找到设置，选择工具，选中File Watcher，点击`+`，选择模板Less，添加一个watcher

![image-20230605210434124](https://pic.imgdb.cn/item/647ddd631ddac507cc1e5ebf.webp)

（2）在打开的新建选项卡中给watcher添加一个名字，可以自定义，文件类型就是Less样式表，程序一般会自动选择lessc，如果没有自动配置，点击后面的文件夹图标可以手动选择。全局安装的less在全局的node_modules中，具体位置看自己安装node时的位置设置。

实参和输出位置根据自己的需要自定义，配置好后点击确定即可

![image-20230605210759461](https://pic.imgdb.cn/item/647dde301ddac507cc20c1cc.webp)

## 测试是否配置成功

随便新建一个less文件，看能否正确编译出css

![image-20230605212114745](https://pic.imgdb.cn/item/647de14d1ddac507cc29ed8c.webp)