---
title: hexo + github 搭建自己的个人博客网站
date: 2017-07-03 16:31:40
categories: study
tags:
---

## 步骤如下：

* 安装 git
``` bash
$ sudo add-apt-repository ppa:git-core/ppa
$ sudo apt-get update
$ sudo apt-get install
```
##### git安装完成后，检查是否安装成功
git –version显示 git version 1.9.1，表明安装成功。

* 安装 git ([nodejs下载地址](https://nodejs.org/en/))
![](/images/nodejs.png)

安装nodejs的方式有多种，我选择了下载编译好的文件进行安装（我下载的版本是：node-v6.11.0-linux-x64.tar.xz）
``` bash
$ sudo tar xf node-v6.11.0-linux-x64.tar.xz -C /usr/local/
$ cd /usr/local/
$ sudo mv node-v5.10.1-linux-x64/ nodejs
$ sudo ln -s /usr/local/nodejs/bin/node /usr/local/bin
$ sudo ln -s /usr/local/nodejs/bin/npm /usr/local/bin
```
##### nodejs安装完成后，检查是否安装成功
###### node -v显示 v6.11.0，表明nodejs安装成功。
###### npm -v显示 3.10.10，表明npm安装成功。

* 安装 hexo
``` bash
$ sudo npm install hexo-cli -g （卸载命令：npm uninstall hexo-cli）
$ hexo init blog
$ cd blog
$ npm install
$ hexo server （启动hexo服务器，默认端口：4000）
```
如果执行hexo出现：hexo: command not found，我的解决办法如下：
``` bash
$ sudo ln -s /usr/local/nodejs/bin/hexo /usr/local/bin
```

执行完上面三步基本上hexo的安装算是完成了，接下来就是部署hexo到github网站上了
1. github网站上的注册或者登陆就省略了，按步骤走就行
2. 现在我们需要_config.yml文件，来建立关联，命令：
``` bash
$ vim _config.yml.
```
翻到最下面，改成我这样子的
```
deploy:
     type: git
     repo: https://github.com/yourname/yourname.github.io.git
     branch: master
```
然后执行命令：
``` bash
$ npm install hexo-deployer-git --save
```
最后，执行配置命令：
``` bash 
$ hexo deploy
```
然后再浏览器中输入 https://yourname.github.io/ 就可以浏览效果了

### 部署步骤
每次部署的步骤，可按以下三步来进行。
``` bash 
$ hexo clean
$ hexo generate
$ hexo deploy
```