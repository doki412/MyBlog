---
title: git入门
date: 2018-05-10 16:17:44
tags:
---
# git init
## 功能：
git仓库的初始化操作，此命令在当前目录下新建一个git仓库。
## 使用：
例子：进入一个空目录git-demo-0，执行``git init``命令，这时该目录下会出现一个隐藏子目录.git（用``ls -la``命令可以查看git-demo-0目录的变化），这是一个空仓库，但是该目录不是空的。

![git init一下，创建一个空仓库.git](http://ww1.sinaimg.cn/large/abbc1cebly1fr6bt8m1uhj20mo07u0uk.jpg)

# git add
## 功能：
将仓库中文件变动更新到暂存区
## 使用：
例子：在git-demo-0目录下新建文件index.html，``git status -sb``一下（查看仓库的状态）会发现仓库中多了该文件，但是如果新建目录 ``mkdir 1`` 再``git status -sb``不会看到有目录更新。

``git add``一下，再``git status -sb``一下查看仓库状态，会发现html文件前面由？？变成了A，即表示更新成功。

![](http://ww1.sinaimg.cn/large/abbc1cebly1fr6ctz4k5nj20l70jr10s.jpg)

# git commit -v
## 功能：
提交仓库变动
## 使用：
进入vim的编辑器界面，具体显示本次提交进行了那些改变。

![](http://ww1.sinaimg.cn/large/abbc1cebly1fr6dsbfd2xj20sw0nuk5p.jpg)

