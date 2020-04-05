---
title: git
date: 2020-03-26 23:02:28
tags:
categories: git
---

## 如何修改最近一次提交注释信息

1、修改本地最近一次提交记录,进入`vim`编辑模式

`git commit --amend`
或
`git commit --amend -m "remove helloworld lane"`

{% asset_img WX20200321.png 1 %}

2、强制覆盖远程最近一次提交记录(特别注意远程其他人是否已经提交了代码)

`git push origin master --force`

{% asset_img WX20200322.png 2 %}

## 不小心提交了重要信息到远程仓库，如何抢救
1、我们假设`remove helloworld lane`这次提交有重要信息，他已经在远程分支了。

{% asset_img WX20200323.png 3 %}

2、我们需要在这条分支的前一次提交那里，选择重置，软合并。

{% asset_img WX20200324.png 4 %}

{% asset_img WX20200325.png 5 %}

3、强制覆盖远程最近一次提交记录(特别注意远程其他人是否已经提交了代码)
`git push origin master --force`

## 撤销未发布的提交
命令行：`git reset —hard HEAD^` 或者 `git reset —hard @{1}`
sourcetree: 右击—》将master重置到这次提交-》混合合并

## 查看文件记录和状态
`git status —short`
`git status —short —gitignored`

## 查看修订版本的差异
 1、比较工作区和暂存区的差别
`git diff`

2、查看暂存区和提交的差别
`git diff —staged (git diff —cached)`

3、查看工作区和提交的区别
`git diff HEAD`

## 一个仓库拥有多个分支
`git checkout --orphan gh-pages`

## 分支使用
新建：`git branch testing`
切换：`git checkout testing`
切换匿名分支：`git checkout —detach 3ead34d `
从匿名分支回到原来分支： `git checkout -`




