---
layout: post
title:  "GIT 基础命令 (2)"
date:   2020-05-02 10:23:28 +0800
categories: git
---

[”GIT 基础命令 (1)"](https://shenjianzhang.github.io/other/2020/04/29/Basic-GIT-Commands.html)中列出的命令足以完成Git在本地仓库(repository)进行版本管理的基本操作，这篇文章则以Git最常见的远程仓库托管网站[GitHub](https://www.github.com)为例，展示如何利用远程仓库(remote repository)来进行版本管理，如何在本地仓库(local repository)和远程仓库(remote repository)之间进行同步，以及如何进行合作的项目开发。

## 远程仓库——Github
在开始我们的远程工作之前，我们首先要在[GitHub](https://www.github.com)注册一个自己的账户，具体的步骤可以参考GitHub的官方帮助手册中["Signing up for GitHub"](https://help.github.com/en/github/getting-started-with-github/signing-up-for-github)部分。

注册成功之后，登录并填写基本信息，首先在自己账户中建立一个全新的仓库(repository)，名为`GitExample`:
![github-create-repository](/img/github-create-repository.png)
GitHub为我们初始化好了这个仓库(repository)，并提示我们可以通过不同方式向其中添加文件
![github-setup-repository](/img/github-setup-repository.png)
我们选择 **“push an existing repository from the command line”** 来将本地仓库(local repository)中的文件和提交(commit)记录同步到GitHub中。根据网页上的提示，我们先进入本地仓库(local repository)，然后用`git remote add <shortname> <url>`将GitHub中刚刚建立的仓库(repository)设为对应的远程仓库(remote repository)
```
$ cd ~/Desktop/GitExample
$ git remote add origin https://github.com/shenjianzhang/GitExample.git
```
需要注意的是，网址中” *shenjianzhang* ”为我在GitHub中的账户名称。之后可以用`git remote -v`来查看远程仓库(remote repository)是否添加成功
```
$ git remote -v
origin	https://github.com/shenjianzhang/GitExample.git (fetch)
origin	https://github.com/shenjianzhang/GitExample.git (push)
```
上面所示的结果即表明已经成功配置了一个URL为“https://github.com/shenjianzhang/GitExample.git”，简称为`origin`远程仓库(remote repository)，这里简称`origin`为Git默认的远程仓库简称，当你拥有多个远程仓库或确实需要(这里的确实需要也可以理解为：我乐意就好)将某个远程仓库特殊命名时，可以在`git remote add`中使用任意简称。简称的作用就是，在之后一些本地仓库和远程仓库的互动命令中，可以用其来代表远程仓库的URL地址(这里暂不考虑SSH通信的情况，详情可以参考[Git官方帮助手册](https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh)。

接下来我们就把我们本地仓库(local repository)中的内容推送到远程仓库(remote repository)中
```
$ git push -u origin master
```
在输入我们在GitHub的用户名和密码后(如果设置好了SSH通信，可以利用SSH-key来实现免密登录)，就会看到本地仓库推送到远程仓库的过程
```
Counting objects: 16, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (13/13), done.
Writing objects: 100% (16/16), 1.59 KiB | 407.00 KiB/s, done.
Total 16 (delta 6), reused 0 (delta 0)
remote: Resolving deltas: 100% (6/6), done.
To https://github.com/shenjianzhang/GitExample.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```
提示信息中最后三行是`git push`命令中`-u`选项的结果，用来将当前本地仓库的分支(branch) “master”与远程仓库的分支(branch)"master"联系起来，这样在使用`git pull`拉取远程仓库内容时，不再需要额外选项。尝试运行
```
$ git pull origin master
```
得到输出
```
From https://github.com/shenjianzhang/GitExample
 * branch            master     -> FETCH_HEAD
Already up to date.
```
此时本地仓库的"master"分支和远程仓库的”master"分支已经完全同步了。

## 其他/未完待续
到目前为止，我个人工作时用到的关于Git的基本操作和基础理解就是这些了，而对Git来说，可能会用到的，还没有理解很好的一大部分，就是关于 **分支(branch)** 的内容，有时间认真学习实践之后再来更新。
