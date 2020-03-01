---
title: 利用Git Hooks实现Hexo部署到VPS
date: 2020-03-01 13:57:35
tags:
    - tutorials
---

在客户端使用 Hexo 生成静态文件，通过 Git 推送到 VPS 的 Git 仓库。在 VPS 中配置 Git Hooks，将静态文件同步到站点目录，实现 Hexo 博客的自动持续更新。

## 本机准备工作
- 安装 Hexo 环境
- 安装 Git
- 生成 ssh 密钥

## VPS 配置工作
VPS 以 Ubuntu18.04 为例，使用 Core Shell连接到 VPS，登录 root 账户。

### 安装 Git
```
git --version    #查看是否安装了git
apt install git  #安装git
```

### 新建用户
新建一个 git 用户，用于推送内容到 vps 的 git 仓库中。
```
adduser git    #新建git用户
```
在 vim 编辑器配置 sudoers 文件，找到如下行
```
vim /etc/sudoers
```
```
# User privilege specification
root    ALL=(ALL:ALL) ALL
```
在下面新增一行
```
git     ALL=(ALL:ALL) ALL
```
保存后退出`:wq!`

### 配置 ssh 公钥登录
```
su git
cd ~
mkdir .ssh && cd .ssh
touch authorized_keys
vim authorized_keys    #将本地 ssh 公钥粘贴进此文件
```
粘贴好公钥之后，即可进行 ssh 连接测试，在终端命令行中输入 `ssh git@ip`(这里的ip是VPS的公网ip地址)，如果能免密登录远程主机，则表示配置成功。

### 修改网页目录的权限
```
mkdir /wwwroot/html/blog              #新建 blog 目录
chown git:git -R /wwwroot/html/blog   #赋予权限
```

### 新建 Git 仓库
```
cd ~
mkdir hexo.git && cd hexo.git
git init --bare                #初始化 git 仓库
```

### 配置 Git Hooks
```
su git
cd /home/git/hexo.git/hooks
touch post-receive             #新建脚本文件
```
在 vim 中编辑`post-receive`文件，输入一下代码后保存退出（`:wq`）
```
#!/bin/sh
git --work-tree=/wwwroot/blog --git-dir=/home/git/blog.git checkout -f

# work-tree 为网站根目录
# git-dir 为 git 仓库目录
```

## 客户端打包部署
进入本地 Hexo 文件夹，打开配置文件`_config/yml`，配置`deploy`项
```
deploy:
    type: git
    repo: git@ip:/home/git/blog.git 
    branch: master
    
# repo中 ip 为VPS的公网ip地址
```
配置完成后，通过`hexo g && hexo d`来将本地文件 push 到 vps 的 git 仓库中，如果一切正常，则说明已经成功，之后即可通过域名访问博客查看内容了。

## 安全问题
搭建 git 服务器后创建一个 git 用户，任何用户都可以使用这个账户来 clone 或 push 数据到仓库中，在本例中，git 仅作为 commit & push 的作用，如果允许其登录 shell，则会存在一定风险和安全隐患，所以需要禁止 git 账户登录 shell，方法如下：
使用 vim 编辑`etc/passwd`这个文件，找到 git 用户的相关行，并修改保存。
```
git:x:1004:1004:,,,:/home/git:/bin/bash
        将其改为↓
git:x:1004:1004:,,,:/home/git:/usr/bin/git-shell
```
之后使用 `ssh git@ip` 来登录的时候就会出现如下信息拒绝 git 用户登录。
```
fatal: Interactive git shell is not enabled.
hint: ~/git-shell-commands should exist and have read and execute access.
Connection to IP closed.
```

至此就完成了通过建立 Git 仓库，使用 Git Hooks来持续部署博客到 VPS 中。

&&
end

---