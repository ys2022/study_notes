# git学习

## 概念
![工作原理/流程：](https://pic2.zhimg.com/80/v2-3bc9d5f2c49a713c776e69676d7d56c5_1440w.jpg)
Workspace：工作区
Index / Stage：暂存区
Repository：仓库区（或本地仓库）
Remote：远程仓库

1. 工作区：就是你在电脑上看到的目录，比如目录下testgit里的文件(.git隐藏目录版本库除外)。或者以后需要再新建的目录文件等等都属于工作区范畴。
2. 版本库(Repository)：工作区有一个隐藏目录.git,这个不属于工作区，这是版本库。其中版本库里面存了很多东西，其中最重要的就是stage(暂存区)，还有Git为我们自动创建了第一个分支master,以及指向master的一个指针HEAD。

## 初始化

```git
$ git config --global user.name "dfsfsfs"
$ git config --global user.email "1360818497@qq.com"
# 显示当前的Git配置
$ git config --list
```

## 一、创建版本库repository

```git
$ mkdir xxx
$ cd xxxx
$ git init 
#建立仓库
```

## 二、基本操作

## git常用命令

```git
#添加到缓存区
$ git add 文件名
#提交到本地库
$ git commit -m "日志信息" 文件名
#查看状态
$ git status 
#查看区别
$ git diff readme.txt 
#查看详细日志
$ git log 
#查看精简历史记录，获取版本号
$ git reflog
#版本回退至100个前的版本
$ git reset --hard HEAD~100
#回退版本号至6fcfc89
$ git reset --hard 6fcfc89
#创建分支
$ git branch 分支名
#查看分支
$ git branch -v
#切换分支
$ git checkout 分支名
#把指定分支合并到当前分支上
$ git merge 分支名
```

### 增加/删除文件

```git
# 添加指定文件到暂存区
$ git add [file1] [file2] ... 
# 添加指定目录到暂存区，包括子目录
$ git add [dir] 
# 添加当前目录的所有文件到暂存区
$ git add . 
# 添加每个变化前，都会要求确认 # 对于同一个文件的多处变化，可以实现分次提交
$ git add -p
# 删除工作区文件，并且将这次删除放入暂存区
$ git rm [file1] [file2] ... 
# 停止追踪指定文件，将文件从缓存区删除，但文件会留在工作区
$ git rm --cached [file] 
# 改名文件，并且将这个改名放入暂存区
$ git mv [file-original] [file-renamed]
```

### 代码提交

```git
# 提交暂存区到仓库区
$ git commit -m [message] 
# 提交暂存区的指定文件到仓库区
$ git commit [file1] [file2] ... -m [message] 
# 提交工作区自上次commit之后的变化，直接到仓库区
$ git commit -a
# 提交时显示所有diff信息
$ git commit -v
# 使用一次新的commit，替代上一次提交。如果代码没有任何新变化，则用来改写上一次commit的提交信息
$ git commit --amend -m [message] 
# 重做上一次commit，并包括指定文件的新变化
$ git commit --amend [file1] [file2] ...
```
## git远程库
#创建远程库链接
git remote add 别名 链接
#推送本地代码到远程库
git push 别名/链接 分支
#拉取远程库到本地库
git pull
#克隆

#










```git

```

