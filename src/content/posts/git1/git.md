---
title: Git命令合集
published: 2022-06-22 14:29:00
image: ./35.avif
tags: [ Git, Git命令 ]
category: 技术笔记
draft: false
---

# Git从入门到精通

## Git简介

Git是一个开源的分布式版本控制系统，用以有效、高速的处理从很小到非常大的项目版本管理。

**Git的特点**

- 分支更快、更容易。
- 支持离线工作；本地提交可以稍后提交到服务器上。
- Git 提交都是原子的，且是整个项目范围的，而不像 CVS 中一样是对每个文件的。
- Git 中的每个工作树都包含一个具有完整项目历史的仓库。
- 没有哪一个 Git 仓库会天生比其他仓库更重要。

Git 是用于 Linux内核开发的版本控制工具。与常用的版本控制工具  CVS, Subversion  等不同，它采用了分布式版本库的方式，不必服务器端软件支持（wingeddevil注：这得分是用什么样的服务端，使用http协议或者git协议等不太一样。并且在push和pull的时候和服务器端还是有交互的。），使源代码的发布和交流极其方便。 Git 的速度很快，这对于诸如 Linux kernel 这样的大项目来说自然很重要。 Git 最为出色的是它的合并跟踪（merge tracing）能力。

实际上内核开发团队决定开始开发和使用  Git 来作为内核开发的版本控制系统的时候，世界开源社群的反对声音不少，最大的理由是 Git 太艰涩难懂，从 Git  的内部工作机制来说，的确是这样。但是随着开发的深入，Git 的正常使用都由一些友好的脚本命令来执行，使 Git  变得非常好用，即使是用来管理我们自己的开发项目，Git 都是一个友好，有力的工具。现在，越来越多的著名项目采用 Git 来管理项目开发。

**Git 与 SVN 区别**

- GIT是分布式的，SVN不是
- GIT把内容按元数据方式存储，而SVN是按文件
- GIT分支和SVN的分支不同
- GIT没有一个全局的版本号，而SVN有
- GIT的内容完整性要优于SVN

**Git的缺点**

- 学习资料少。
- 学习周期相对而言比较长。
- 不符合常规思维。
- 代码保密性差。



## 安装Git

肯定是装window版本

下载地址:https://git-scm.com/downloads（官网）


## 创建项目

步骤省略....

## 创建仓库

* 配置git

Git 全局设置:

```shell
git config --global user.name "ange"
git config --global user.email "1351261434@qq.com"
```

* 实战

配置idea中的过滤文件

```tex
*.hprof;*.idea;*.iml;*.pyc;*.pyo;*.rbc;*.yarb;*~;.DS_Store;.git;.hg;.svn;CVS;__pycache__;_svn;target;vssver.scc;vssver2.scc;
```
* Git常用命令

```shell
#初始化git仓库
git init
#查看git文件状态(查看文件是否被git追踪)
git status
#查看所有本地分支 前面带有*号的是当前分支
git branch
#查看所有远程分支
git branch -r
#查看所有本地和远程分支
git branch -a
#创建分支
git branch 分支名
#切换分支
git checkout 分支名、
#切换分支并且转换过去
git checkout -b 新分支名
#分支模糊查找
git branch | grep 分支名
#删除本地分支（D 强制）
git branch -D 分支名
#删除远程分支
git push origin --delete 分支名
#如果没有被追踪
git add <file>...
git add pom.xml
#撤销追踪
git rm --cached <file>
git rm --cached pom.xml
#全部进行追踪
git add .
#提交到本地仓库
git commit -m "提交的消息"
#查看是否配置远程仓库
git remote -v
#设置远程仓库地址
git remote add origin https://gitee.com/AngeGit/springboot_miaosha.git
#提交到远程仓库
git push -u origin master
#第一次使用仓库需要先pull再push 所以这个时候可以进行强制合并，用下边的方式就OK了。
//把远程仓库和本地同步，消除差异
git pull origin master --allow-unrelated-histories 
#删除缓存区指定文件
git rm --cached readme.txt
#清空缓存区
 rm .git/index

#克隆远程地址的项目
git clone https://gitee.com/AngeGit/springboot_miaosha.git
#重复上述步骤
#拉取远程仓库的代码
git pull
```

## IDEA操作git

## 分支操作

```shell
#提交代码
git add .
#提交到本地仓库
git commit -m "消息"
#查看是否有远程仓库
git remote -v
#提交到远程仓库
git push -u origin test

#修改远程仓库地址
git remote set-url origin 远程仓库地址

#切换分支
git branch
git checkout master
#合并
git merge test
git push -u origin master
```

