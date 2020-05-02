---
layout: post
title:  "GIT 基础命令 (1)"
date:   2020-04-29 21:32:28 +0800
categories: other
---

[**Git**](https://git-scm.com/) 是一款免费开源的分布式版本管理系统(free and open source distributed version control system)。在我日常工作中，使用到的场景主要为代码更新时的版本控制，以及与[Github](https://github.com/)的交互。通俗来说就是记录每一次代码修改的内容，通过比较修改细节以发现出现问题的原因或代码位置，从而在需要时合并不同版本(覆盖旧的版本)，或恢复到特定修改节点(Git saves single changes for each document and can be used to merge multiple version of one document.)。

这系列文章从建立一个全新的Git仓库(repository)开始，记录了一个个人工作项目的创建和管理过程，并对其中使用的Git命令进行了介绍。文章更多的是一个工作过程的记录，关于Git的详细介绍可以参考官网给出的[《Pro Git》](https://git-scm.com/book/zh/v2)丛书。网上也有很多对于Git的简单介绍和命令说明，这里给出几个自己参考过的网站：
- Git教程及练习:<https://swcarpentry.github.io/git-novice/>
- Git命令:<http://ndpsoftware.com/git-cheatsheet.html>
- Git命令行教程(15-30min):<https://try.github.io/>

本文主要参考 <https://swcarpentry.github.io/git-novice/> 中的教程，感谢 *Software Carpentry* <http://software-carpentry.org/>制作并分享了这一教程。

## 安装
在Ubuntu系统上，可以利用`apt`命令来安装Git。
```
$ sudo apt-get insatll git-all
```
对于其他Linux发行版，官网给出了相应命令，详见<https://git-scm.com/download/linux>。

安装成功后，运行命令
```
$ git --version
```
可以查看当前Git版本。

## 设置全局参数
在具体创建项目之前，我们先配置自己的Git，其中较为重要的是用户信息
```
$ git config --global user.name "UserName"
$ git config --global user.email "example@example.com"
```
除此之外，我们还可以指定Git所使用的文本编辑器，如*vim*(否则为系统默认的编辑器)
```
$ git config --global core.edito vim
```
更多Git配置信息可以参考 <https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration>

## 第一个仓库
在创建第一个仓库(repository)之前，我们首先需要了解Git的基本思路，简单来说，仓库(repository)是Git进行版本控制的“位置”和基础，我们可以在仓库(repository)中进行文件的跟踪(track)，并暂存(stage)或提交(commit)更改，或比较文件的不同。
首先，我们在某一位置(如`Desktop`)建立一个文件夹`GitExample`，并进入该文件夹
```
$ cd ~/Desktop
$ mkdir GitExample
$ cd GitExample
```
之后将`GitExample`文件夹初始化为一个Git仓库(repository)
```
$ git init
```
虽然`ls`命令发现`GitExample`文件夹中没有任何变化，但是运行`ls -a`之后，可以看到文件中多了一个隐藏文件夹`.git`，其中便存储着Git对于这个仓库(repository)中项目的管理信息。同时，我们还可以看到命令行当前位置信息处多了`<master>`标记，这表示当前仓库(repository)中的分支(branch)信息，关于分支(branch)，可以理解为同一项目的不同版本，通过合并(merge)分支(branch)可以实现对版本的覆盖或修改。

在初始化仓库(repository)之后，我们可以通过`git status`命令来查看当前项目状态
```
$ git status
```
结果如下
```
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```
此外，由于`.git`中存储着Git的具体信息，当我们想删除某一个Git仓库(repository)时，可以直接通过删除`.git`来实现
```
$ rm -rf .git
```
从而只删除Git仓库(repository)而保留原文件夹中的其他文件。

## 跟踪文件修改
这一部分可以看作是个人利用Git进行版本管理的关键部分。
我们在`~/Desktop/GitExample`中，建立一个新的文本文件`earth.txt`
```
$ vim earth
```
输入以下文字并保存。
```
Earth is the third planet from the Sun and the only astronomical object known to harbor life.
```
之后再次查看Git中项目状态
```
$ git status
```
可以看到Git已经发现了新建文件`earth.txt`
```
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	earth.txt

nothing added to commit but untracked files present (use "git add" to track)
```
"Untracked files"表示这个文件虽然在当前文件夹中，但是Git并没有对它进行跟踪(track),我们可以使用命令`git add`来让Git跟踪(track)这一文件
```
$ git add earth.txt
```
这样`earth.txt`便被跟踪(track)，并处于暂存(stage)状态，再次使用`git status`查看项目状态
```
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   earth.txt
```
我们可以看到`earth.txt`不再是`untracked`状态，而是`changes to be committed`，这表示其已经被跟踪(track)，但是这一变化(新建文件)并没有被提交(commit)到本地的仓库(repository)中。我们利用命令`git commit`来完成提交(commit)
```
$ git commit -m "First Commit"
```
得到输出
```
[master (root-commit) 2bc595f] First Commit
 1 file changed, 1 insertion(+)
 create mode 100644 earth.txt
```
`git commit`可以认为是将`git add`暂存的操作记录下来并在`.git`中做一份永久拷贝，这一份永久拷贝就被称作一个 *提交(commit)* ，这里的 *提交(commit)* 作为名词，可以看作是提交(commit)操作的结果，即本地仓库(repository)中记录的文件变化集(changeset)，在上面例子中这个变化集(changeset)就是新建了文件`earth.txt`并在其中输入了`Earth is the third planet ...`这句话。如果我们使用`git add`暂存(stage)了多个文件的变更，那么`git commit`所记录的变化集(changeset)就是这多个文件变更的合集。

在上面提交(commit)时，`-m`选项后是对这次提交(commit)的简要描述，这个描述可以帮助我们在之后回看此次提交(commit)时理解提交(commit)中的操作和其目的。

如果我们只是运行`git commit`而不加`-m`选项，Git会自动打开`core.editor`中定义的文本编辑器，我们可以在文本编辑器中输入对提交(commit)的描述，第一行是简要介绍，与`-m`后描述相同，尽量少于50个字符，空一行之后，还可以输入一些附加信息，保存并退出文本编辑器，这次提交(commit)也就完成了。

此外，在`git commit`的输出中，我们还可以看到此次提交(commit)的短编号(ID)，例子中为`2bc595f`。

现在再次查看仓库(repository)的状态
```
$ git status
On branch master
nothing to commit, working tree clean
```
可以看到在当下仓库(repository)中，所有文件都被跟踪(track)，而且所有最新的变化也被Git记录了下来。

接下来，我们向`earth.txt`中添加一行
```
$ cat earth.txt
Earth is the third planet from the Sun and the only astronomical object known to harbor life.
According to radiometric dating and other evidence, Earth formed over 4.5 billion years ago.
```
并查看仓库(repository)的状态
```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   earth.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
从输出信息中我们也可以看到，Git发现文件`earth.txt`已经被修改(modified)，但是并没有被暂存(stage)或提交(commit)。

在我们暂存(stage)或提交(commit)修改后的`earth.txt`之前， 我们可以先利用`git diff`命令查看文件没有暂存(unstaged)的状态和上次提交(commit)的状态之间的区别
```
$ git diff
```
输出如下
```
diff --git a/earth.txt b/earth.txt
index d81919d..26cc36a 100644
--- a/earth.txt
+++ b/earth.txt
@@ -1 +1,2 @@
 Earth is the third planet from the Sun and the only astronomical object known to harbor life.
+According to radiometric dating and other evidence, Earth formed over 4.5 billion years ago.
```
值得注意的是，`git diff`只能显示尚未暂存(stage)的改动，也就是说如果用`git add`暂存(stage)了文件，那么`git diff`后不会有输出。而`git diff --staged`可以输出暂存(stage)文件和最后一次提交(commit)的文件之间的差异。

我们再次将对`earth.txt`的修改暂存(stage)并提交(commit)。
```
$ git add earth.txt
$ git commit -m "Add the age of the Earth."
```
提交(commit)之后，我们可以利用命令`git log`来查看我们的提交(commit)历史。
```
$ git log
```

如果我们在项目编辑过程中想移除一些不需要或者错误暂存(stage)或提交(commit)的文件，需要使用  `git rm`命令。为此，我们首先在工作目录中创建一个新的文本文件`moon.txt`，内容如下
```
cat moon.txt
The Moon is an astronomical body orbiting Earth as its only natural satellite.
```
并将其暂存(stage)
```
$ git add moon.txt
```
运行`git status`可以发现`moon.txt`已经是”Changes to be committed”状态。

如果我们只是想把文件从本地仓库(repository)或暂存(stage area)中移除，而保留在工作目录中的文件本身，即不再让Git跟踪(track)这个文件，可以用`git rm --cashed`命令
```
$ git rm --cached moon.txt
```
再运行`git status`看到`moon.txt`又回到“Untracked files”的状态。如果`moon.txt`已经被提交(commit)过，即处于“Unmodified”或“modified”状态，在用`git rm --cached`删除之后，`git status`的输出为(这里需要先通过`git add`和`git commit`对`moon.txt`进行提交)
```
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	deleted:    moon.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	moon.txt
```
可以看出还需要将这一删除操作进行提交(commit)，即
```
$ git commit -m "Delete moon.txt"
```
才彻底放弃对`moon.txt`的跟踪(track)，并将这一操作记录下来。

另一方面，如果我们要将一个文件从工作目录中删除，假如这个文件已经被Git所跟踪(track)，那么仅仅使用`rm`删除文件本身是不够的，还需要让Git记录这次移除，为此我们将`moon.txt`再次暂存(stage)，然后用`rm`删除文件，在用`git rm`移除记录
```
$ git add moon.txt
$ rm moon.txt
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   moon.txt

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	deleted:    moon.txt
$ git rm moon.txt
```
同样，对于已经被提交(commit)过的文件，`git rm`的移除操作其实相当于处于暂存区域(stage area)，需要通过提交(commit)来记录。

在这一部分的最后，我们来总结一下Git对于文件的操作。对于一个文件，其状态可以是
- *项目的工作文件夹(project’s working directory)*，其对于Git来说可以是未跟踪(untracked)状态，也可以是已跟踪(tracked)状态，但是文件在上次被提交(commit)之后进行了修改，这个修改尚未进入暂存区域(stage area);
- *暂存区域(stage area)*，在`git add`之后，文件成为跟踪(tracked)状态，这部分的更改将会构成下一次的提交(commit);
- *本地仓库(local repository)*，`git commit`后，提交(commit)在这里被永久记录下来，一个个提交(commit)就是对于项目更改过程的一次次快照。

![image01](/img/git-staging-area.svg)

(引自：<https://swcarpentry.github.io/git-novice/04-changes/index.html>



## 回溯项目历史
我们继续向`earth.txt`中添加一行，并将第一行的`Earth`改为`EARTH`
```
$ cat earth.txt
EARTH is the third planet from the Sun and the only astronomical object known to harbor life.
According to radiometric dating and other evidence, Earth formed over 4.5 billion years ago.
Earth's gravity interacts with other objects in space, especially the Sun and the Moon, which is Earth's only natural satellite.
```
我们首先比较文件`earth.txt`当前状态和最近一次提交(commit)时的不同，**注意这里我们用 *HEAD* 来表示最后一次提交(commit)**。
```
$ git diff HEAD earth.txt
```
得到结果
```
diff --git a/earth.txt b/earth.txt
index 26cc36a..8f75253 100644
--- a/earth.txt
+++ b/earth.txt
@@ -1,2 +1,3 @@
-Earth is the third planet from the Sun and the only astronomical object known to harbor life.
+EARTH is the third planet from the Sun and the only astronomical object known to harbor life.
 According to radiometric dating and other evidence, Earth formed over 4.5 billion years ago.
+Earth's gravity interacts with other objects in space, especially the Sun and the Moon, which is Earth's only natural satellite.
```
如果想要比较文件`earth.txt`当前状态和倒数第二次提交(commit)时的不同,则可以用`HEAD～1`来表示最近一次提交(commit)之前的那次提交(commit)。以此类推，对于有多次提交(commit)的项目中的文件，我们可以用`HEAD～1`，`HEAD～2`等来表示最近的几次提交(commit)记录。由于最近几次提交(commit)都是关于`monn.txt`的修改，通过查看`git log`的记录，可以找到再上一次对于`earth.txt`的修改为`HEAD～5`
```
$ git diff HEAD~5 earth.txt
```
得到结果
```
diff --git a/earth.txt b/earth.txt
index d81919d..8f75253 100644
--- a/earth.txt
+++ b/earth.txt
@@ -1 +1,3 @@
-Earth is the third planet from the Sun and the only astronomical object known to harbor life.
+EARTH is the third planet from the Sun and the only astronomical object known to harbor life.
+According to radiometric dating and other evidence, Earth formed over 4.5 billion years ago.
+Earth's gravity interacts with other objects in space, especially the Sun and the Moon, which is Earth's only natural satellite.
```
如果我们只是想查看某次提交(commit)的内容和所做的修改，则运行命令`git show`
```
$ git show HEAD～4 earth.txt
```
得到结果
```
commit 7dc0549cd4e5a4f86135a9a716e07a5d7322a3ce
Author: shenjianzhang <sjzhang@pku.edu.cn>
Date:   Thu Apr 30 21:06:11 2020 +0800

    Add the age of the Earth.

diff --git a/earth.txt b/earth.txt
index d81919d..26cc36a 100644
--- a/earth.txt
+++ b/earth.txt
@@ -1 +1,2 @@
 Earth is the third planet from the Sun and the only astronomical object known to harbor life.
+According to radiometric dating and other evidence, Earth formed over 4.5 billion years ago.
```
正如前面看到的，其实对于每一次提交(commit)，Git都会生成一个独有的ID，例如上面`HEAD～4`代表的这次提交(commit)的ID为"**7dc0549**cd4e5a4f86135a9a716e07a5d7322a3ce"，通过`git log`同样可以查到每次提交(commit)的ID，这样我们就可以利用这个ID，**或者ID的前7位**，来表示对应的提交(commit)，从而进行查看和比较。
```
$ git diff 7dc0549 earth.txt
```
得到输出
```
diff --git a/earth.txt b/earth.txt
index 26cc36a..8f75253 100644
--- a/earth.txt
+++ b/earth.txt
@@ -1,2 +1,3 @@
-Earth is the third planet from the Sun and the only astronomical object known to harbor life.
+EARTH is the third planet from the Sun and the only astronomical object known to harbor life.
 According to radiometric dating and other evidence, Earth formed over 4.5 billion years ago.
+Earth's gravity interacts with other objects in space, especially the Sun and the Moon, which is Earth's only natural satellite.
```
除了查看和比较之前的提交(commit)记录，我们还可以尝试利用`git checkout`来恢复到某一次提交(commit)时的状态。
```
$ git checkout HEAD~4 earth.txt
```
这时`earth.txt`中的内容即为`HEAD～4`这次提交之后的内容，其在Git中也不再是“modified”的状态。
```
$ cat earth.txt
Earth is the third planet from the Sun and the only astronomical object known to harbor life.
According to radiometric dating and other evidence, Earth formed over 4.5 billion years ago.
$ git status
On branch master
nothing to commit, working tree clean
```
即使`earth.txt`位于暂存(stage)状态，`git checkout`也会将文件恢复到特定的提交(commit)之后的状态。

需要注意的是，在使用`git checkout`来恢复某一个文件的状态时，一定要加上文件名，否则Git跟踪(track)的所有文件都会被恢复到某次提交(commit)之后的状态，对其他文件所做的修改也会被重写，也就是处于`detached HEAD`状态，这是很危险的。

最后，对于我们错误提交(commit)的记录，我们可以用`git revert [erroneous commit ID]`来新建一个提交(commit)来取消那次错误的提交(commit)。

## 忽略
对于一些我们工作中不需要进行跟踪的文件或文件夹，我们可以使用文件`.gitignore`文件来设置Git的忽略规则。例如我们在程序编译时产生的`*.o`文件和`/bin`文件夹中的所有文件并不需要被Git所跟踪，我们新建一个名为`.gitignore`的文件，输入`*.o`和`bin/`，保存并退出。之后我们将`.gitignore`提交(commit)
```
$ cat .gitignore
*.o
bin/
$ git add .gitignore
$ git commit -m "Ignore *.o files"
```
之后我们在暂存(stage)目录中文件时，当前目录中的所有`*.o`文件和`/bin`中的所有文件都不会进入暂存区域(stage area)，如果运行`git add example.o`，Git也会提示我们这一文件被`.gitignore`中的规则所忽略。
