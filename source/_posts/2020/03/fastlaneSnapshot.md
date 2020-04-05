---
title: fastlaneSnapshot
date: 2020-03-22 15:08:07
categories: 持续构建
---

[中文文档](https://s0docs0fastlane0tools.icopy.site/getting-started/ios/screenshots/)
[英文文档](https://docs.fastlane.tools/getting-started/ios/screenshots/)

## [demo 地址](https://github.com/YUJINHAI2015/FastlaneDemo/tree/master/FastlaneSnapshot)

## 运行环境
- xcode Version 11.3.1 (11C504)
- fastlane Version 2.143.0

## 创建一个项目 `FastlaneSnapshot`
- 用`xcode`新建项目`FastlaneSnapshot`
- 用命令行进入到`FastlaneSnapshot`所在的路径，创建一个文件夹和两个空文件，运行下面命令：

```
$: mkdir fastlane
$: touch fastlane/Appfile
$: touch fastlane/Fastfile

```

## 创建一个 `FastlaneSnapshotUITests` 并按照下图操作
1. `$: fastlane snapshot init`
2. 新建一个`FastlaneSnapshotUITests target`
3. 拖拽`SnapshotHelper.swift` 到 `FastlaneSnapshotUITests`
4. 编辑`FastlaneSnapshotUITests` 的 `scheme`
5. 在 `setUp` 添加代码

{% asset_img snapshotInit.png snapshotInit %}

{% asset_img UITests_Targert.png UITests_Targert %}

{% asset_img DrapHelper.png DrapHelper %}

{% asset_img scheme.png scheme %}

{% asset_img setup.png setup %}

## 运行`fastlane snapshot`

报错：`Exit status: 70`   `Caught error... 70`  -- 猜测是编译版本太高了。
1、13.0的版本太高了，改成10.0
2、删掉一些不必要的代码，确保项目能够编译通过。--记得`build`一下。
3、在命令行中记性运行：`fastlane snapshot`
{% asset_img iosVersion.png iosVersion %}

{% asset_img changeVersion.png changeVersion %}

## 手机型号太多了，运行会很久，我们修改一下`Snapfile`

`&: open fastlane/Snapfile `

{% asset_img selectedDevice.png selectedDevice %}

重新运行 `fastlane snapshot` 这次就快很多了。


## `fastlane` 版本问题
`undefined method 'each' for nil:NilClass` 这个错误就是 版本问题引起的。

- 查看版本 `fastlane --version`
发现`fastlane` 可以通过 `brew`或者`gem`按照，[两者区别](https://www.cnblogs.com/ayseeing/p/3610777.html),
而我现在是通过`brew`安装的，版本是 2.28.3。而且一直报上面的错误，更新到最新也不行：`brew upgrade fastlane`
现在尝试用`gem`来安装看看。

- 先卸载掉`brew`安装的：`brew cask uninstall fastlane`

- 通过`gem`安装： `sudo gem install fastlane`
```
➜  FastlaneSnapshot fastlane --version
fastlane installation at path:
/Library/Ruby/Gems/2.6.0/gems/fastlane-2.143.0/bin/fastlane
-----------------------------
[✔] 🚀 
fastlane 2.143.0

```

## 参考链接：[undefined method 'each' for nil:NilClass](https://github.com/fastlane/fastlane/issues/15496)
