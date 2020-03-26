---
title: git
date: 2020-03-26 23:02:28
tags:
categories: git
---

## 如何修改最近一次提交注释信息
{% WX20200326-232249@2x.png WX20200326-232249@2x %}

1、修改本地最近一次提交记录,进入`vim`编辑模式

`git commit --amend`
或
`git commit --amend -m "remove helloworld lane"`

{% WX20200326-232432@2x.png WX20200326-232432@2x %}

2、强制覆盖远程最近一次提交记录(特别注意远程其他人是否已经提交了代码)

`git push origin master --force`

{% WX20200326-233519@2x.png WX20200326-233519@2x %}

## 不小心提交了重要信息到远程仓库，如何抢救
1、我们假设`remove helloworld lane`这次提交有重要信息，他已经在远程分支了。

{% WX20200326-234410@2x.png WX20200326-234410@2x %}

2、我们需要在这条分支的前一次提交那里，选择重置，软合并。

{% WX20200326-234427@2x.png WX20200326-234427@2x %}

{% WX20200326-234800@2x.png WX20200326-234800@2x %}

3、强制覆盖远程最近一次提交记录(特别注意远程其他人是否已经提交了代码)
`git push origin master --force`
