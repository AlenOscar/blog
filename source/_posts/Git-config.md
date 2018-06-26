---
title: 解决 git push 每次都需要输入用户名和密码
date: 2017-07-08 18:03:16
categories: essay
tags:
---

### Git SSH Key 生成步骤
Git是分布式的代码管理工具，远程的代码管理是基于SSH的，所以要使用远程的Git则需要SSH的配置
一、设置Git的username和email：
``` bash
$ git config --global user.name "your_username"
$ git config --global user.email "your_email"
```
二、生成SSH密钥过程：
1. 查看是否已经有了ssh密钥：
``` bash
$ cd ~/.ssh
```
如果没有密钥则不会有此文件夹，有则备份删除
2. 生成密钥：
``` bash
$ ssh-keygen -t rsa -C “alenoscar@163.com”
```
按3个回车，密码为空。
```
Your identification has been saved in /home/tekkub/.ssh/id_rsa.
Your public key has been saved in /home/tekkub/.ssh/id_rsa.pub.
The key fingerprint is:
………………
```
最后得到了两个文件：id_rsa和id_rsa.pub
3. 添加密钥到ssh：ssh-add 文件名，需要之前输入密码
4. 在github上添加ssh密钥，这要添加的是“id_rsa.pub”里面的公钥
打开https://github.com/ ，登陆alenoscar，然后添加ssh
5. 测试：
``` bash
$ ssh git@github.com
```
```
The authenticity of host ‘github.com (207.97.227.239)’ can’t be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added ‘github.com,207.97.227.239′ (RSA) to the list of known hosts.
ERROR: Hi tekkub! You’ve successfully authenticated, but GitHub does not provide shell access
Connection to github.com closed.
```

### git push 免输用户名和密码设置
1. 在termail里边 输入
``` bash
$ git remote -v
```
origin  https://github.com/AlenOscar/hexo_blog.git (fetch)
origin  https://github.com/AlenOscar/hexo_blog.git (push)
2. 下面把它换成ssh方式的，移出旧的http的origin
``` bash
$ git remote rm origin
```
添加新的git方式的origin
``` bash
$ git remote add origin git@github.com:AlenOscar/hexo_blog.git
```
我们再查看一下push方式
``` bash
$ git remote -v
```
origin  git@github.com:AlenOscar/hexo_blog.git (fetch)
origin  git@github.com:AlenOscar/hexo_blog.git (push)
3. 再次push一下，已经不需要输入用户名密码了
``` bash
$ git push origin 
```
[vagrant@localhost source]$ git push origin
Everything up-to-date
4. 如果 Github遇到 Warning: Permanently added the RSA host key for IP address '192.30.255.112' to the list of known hosts.
警告的大概意思就是：警告：为IP地址192.30.255.112的主机（RSA连接的）持久添加到hosts文件中
解决方法如下：
``` bash
$ sudo vim /etc/hosts
```
添加一行：192.30.255.112　github.com