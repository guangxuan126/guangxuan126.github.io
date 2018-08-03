---
title: Git常用指令整理
date: 2018-01-03 20:58:04
tags:
  - tutorials
---

本文对指令按照使用场景(建库，查看，修改，分支)进行分类归纳，介绍指令基本含义和用法，方便查阅。

### 工作区、版本库和暂存区
   __工作区:__ 即工作目录。
   __版本库:__ 隐藏目录`.git`，这个就是git的版本库。
   __暂存区:__ Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。

将文件向Git版本库里添加时，是分为两步骤进行的：
>1.用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；
>2.用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。

### 本地库和远程库
#### 新建仓库
  &emsp;&emsp;·建立远程库
  &emsp;&emsp;·本地新建文件夹
  &emsp;&emsp;·`git init`初始化仓库，可以发现当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的。__-请勿修改-__
  &emsp;&emsp;·远程库的名字就是`origin`，这是Git默认的叫法
  &emsp;&emsp;·`git remote add origin git@github.com:guangxuan126/demo.git` 这个命令是在本地的demo仓库下执行的。这两个地方的仓库名不需要相同，因为会通过在本地的仓库目录下执行这条命令已经将两者建立了联系
  &emsp;&emsp;·`git push -u origin master` 把本地库的所有内容推送到远程库上。把本地库的内容推送到远程，用`git push`命令，实际上是把当前分支master推送到远程。由于远程库是空的，我们第一次推送master分支时，加上了-u参数(推送和关联，Git不但会把本地的master分支内容推送到远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
  &emsp;&emsp;·`git push origin master`每次本地提交后,推送最新修改到远程库

#### 从远程库克隆
假设github上面已经有一个远程库，但是本地没有，需要克隆到本地，远程库的名字叫`demo2`<br>
  &emsp;&emsp;·`git clone git@github.com:guangxuan126/demo2.git` 克隆一个本地库,则在当前文件夹下会多一个demo2的文件夹。
  &emsp;&emsp;·`cd demo2`进入克隆下来的本地库，默认的名字是和github上的一样的
  &emsp;&emsp;·`git push origin master` 推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上

### 常用查询指令
  &emsp;&emsp;·`git status` 查看仓库当前的状态
  &emsp;&emsp;·`git diff 文件名`查看对文件做什么修改
  &emsp;&emsp;·`git diff 版本号1 版本号2 --stat`查看两个版本的差异的文件列表，包括被修改行数和增删图。参数改为`--name-status`前面显示修改说明字母(A,M等)，无行数
  &emsp;&emsp;·`git log`显示从最近到最远的提交日志
  &emsp;&emsp;·`git log --pretty=oneline` 简化日志输出的显示信息，`commit id`很长
  &emsp;&emsp;·`git reflog` 记录你的每一次命令，最先显示的是这个命令执行之后的版本的版本号的前七位，这样就算你清屏了或者重启了，也能找到某个版本的版本号，就可以轻松回退到那个版本
  &emsp;&emsp;· `git branch` 查看当前所在的分支。git branch命令会列出所有分支，当前分支前面会标一个`*`号
  &emsp;&emsp;·`git log --graph --pretty=oneline --abbrev-commit`用带参数的git log可以看到分支的合并情况。用`git log --graph`命令可以看到分支合并图
  &emsp;&emsp;·`git remote` 查看远程库的信息
  &emsp;&emsp;·`git remote -v` 显示更为详细的信息

### 常用修改指令
  &emsp;&emsp;·`git add readme.md`添加文件，但是不提交
  &emsp;&emsp;·`git commit -m "提交描述"`提交，__只有add后提交才有效。__ _“改文件->add文件->再改->提交”_，则第二次修改无效,不会被提交，只会成功提交第一次的修改。

### 撤销修改和版本回退
  &emsp;&emsp;·`git checkout -- 文件名`把没暂存(即没add)的干掉，或者说，丢弃工作区，回到到暂存状态
  &emsp;&emsp;·`git reset HEAD 文件名`把暂存的状态取消，工作区内容不变，但状态变为“未暂存”。
简单来说，没有add过的修改，只需要`git checkout -- 文件名`即可撤销；add 过的修改，先`git reset HEAD 文件名`变成没add 过的修改，再`git checkout -- 文件名`撤销。
  &emsp;&emsp;·`git reset --hard HEAD^` 会回退到上一个版本
  &emsp;&emsp;·`git reset --hard 某版本号前几位`通过命令行上的历史信息（假如你没清屏的话），找到某版本 的版本号回到指定版本。不一定要全部的版本号，就像这个命令的例子，只要前面的约7、8位这样就可以。

### 分支管理
#### 创建和合并分支
  &emsp;&emsp;·`git checkout -b dev`创建一个新的分支：dev，并且会切换到dev分支。所以这条命令有两个作用。`git checkout`命令加上`-b`参数表示创建并切换，相当于以下两条命令：`git branch dev`和`git checkout dev`
  &emsp;&emsp;·`git branch dev`，新建分支是新建指针,指向当前commit
  &emsp;&emsp;·`git checkout dev`切换到dev分支
  &emsp;&emsp;·`git checkout master`dev分支的工作完成，我们就可以切换回master分支 __(此时在dev分支的修改在master上是看不到的)__
  &emsp;&emsp;·`git merge dev` 这是在master分支上执行的命令，作用是：把dev分支上的工作成果合并到master分支上
  &emsp;&emsp;·`git branch -d dev` 删除已合并的分支。删除分支就是删除指针
  &emsp;&emsp;·`git branch -D dev`Git友情提醒，dev分支还没有被合并，如果删除，将丢失掉修改，如果要强行删除，需要使用`git branch -D dev`命令
  &emsp;&emsp;·`git rebase master`变基。在当前分支(非master)下执行该命令，则相当于把当前分支和mater分支合并，和merge操作类似，但提交历史不同，rebase操作的log更干净

#### 远程分支
  &emsp;&emsp;·`git fetch origin` 这个命令查找 “origin” 是哪一个服务器，从中抓取本地没有的数据，并且更新本地数据库，移动 `origin/master`指针指向新的、更新后的位置
  &emsp;&emsp;·`git push (remote) (branch)`推送本地的分支来更新远程仓库上的 同名分支。如前文提到的`git push origin master`就是将本地master分支推送到远程master分支；复杂一点的，`git push origin serverfix:awesomebranch`将本地的 serverfix分支推送到远程仓库上的awesomebranch分支
  &emsp;&emsp;·`git push origin --delete serverfix`或者`git push origin :remotebranch`,删除远程的serverfix分支
  &emsp;&emsp;·`git pull`在大多数情况下它的含义是一个`git fetch`紧接着一个`git merge`命令。
  <br>
### 推荐优秀教程
> - [Git](https://git-scm.com/book/zh/v2)
> - [Pro Git](http://iissnan.com/progit/)

<br>
&&
end
