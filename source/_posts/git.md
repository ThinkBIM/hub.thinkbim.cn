---
title: Git常用命令
date: 2021-07-19
description: git查看创建删除分支，更改URL，撤销等常用命令操作
keywords: Git|命令|处理分支|更改URL
tags:
  - command
categories:
  - Git
---

[git](https://git-scm.com/) 是一个开源的分布式版本控制系统，可以有效、高速地处理从很小到非常大的项目版本管理。也是Linus Torvalds为了帮助管理Linux内核开发而开发的一个开放源码的版本控制软件

### 查看远端和本地分支

```shell
git branch -a
* main
  master
  remotes/origin/main
  remotes/origin/master

#删除本地分支
git branch -d master
Deleted branch master (was 066fcc4).

#删除远端分支
git push origin --delete master
To https://github.com/HateGhost/ThinkBIM.git
 - [deleted]         master
```

### 更改URL

```shell
git remote -v
origin	https://github.com/HateGhost/ThinkBIM.git (fetch)
origin	https://github.com/HateGhost/ThinkBIM.git (push)
```

```shell
git remote set-url origin https://github.com/ThinkBIM/ThinkBIM.git
```



```shell
git clone -b dev_jk http://10.1.1.11/service/tmall-service.git

```

### 删除分支

> 删除本地分支

```shell
git branch -d localBranchName
```

> 删除远端分支

```shell
git push origin --delete develop
```

### 创建分支



### 克隆指定分支

```shell
git clone -b dev git.thinkbim.cn
```



### 撤销 git add

```shell
git reset --mixed
git reset HEAD .
git reset HEAD 文件
```

### tag

```shell
# 删除本地
git tag -d v1.0 
# 删除远端
git push origin :refs/tags/v1.0
```


## F&Q

```shell
git push origin --delete develop
remote: GitLab: The default branch of a project cannot be deleted.
To git.jxqianbao.com:server/finance.git
 ! [remote rejected] develop (pre-receive hook declined)
error: failed to push some refs to 'git@git.demo.com:server/finance.git'


git clone https://github.com/ThinkBIM/comic.git
Cloning into 'comic'...
fatal: unable to access 'https://github.com/ThinkBIM/comic.git/': Encountered end of file
git config --global --unset http.proxy


```










