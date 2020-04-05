---
title: xcodebuild学习
date: 2020-03-29 21:00:01
tags:
categories: 持续构建
---

[参考地址](https://developer.apple.com/library/archive/technotes/tn2339/_index.html)

### xctool 和xcodebuild
1、xctool 是一款开源软件 `brew install xctool`，本文暂时没有讨论xctool.

2、xcodebuild是苹果自带的,用于编译，打包和测试。

- 查看帮助，看下`xcodebuild`支持哪些命令
`xcodebuild -help`
> `help`列出了两部分，一部分是命令行用到的，另一部分是`export.plist`用到
命令行输入：指定那个workspace，scheme,路径....
`export.plist`：签名证书等...

- 查看项目的`scheme`
`xcodebuild -list -workspace TravisCIDemo.xcworkspace`

- 编译你的项目
`xcodebuild -workspace TravisCIDemo.xcworkspace -scheme TravisCIDemo build`

- 打包你的项目
`xcodebuild -workspace TravisCIDemo.xcworkspace -scheme TravisCIDemo archive`

- 1) 打包项目到指定文件,会生成一个`build`文件
> `xcodebuild -workspace TravisCIDemo.xcworkspace -scheme TravisCIDemo -archivePath build/TravisCIDemo.xcarchive archive`
- 2) 创建一个`export.plist`文件，并添加一个字段，表示打包的类型，常用的有`app-store, ad-hoc, package, enterprise, development, and developer-id`

- 3) 打包，然后就可以在`build`文件中看到api
> `xcodebuild -exportArchive -archivePath build/TravisCIDemo.xcarchive -exportPath build -exportOptionsPlist export.plist`

{% asset_img WX202003291.png 1 %}

{% asset_img WX202003292.png 2 %}

- Build Products Path
`xcodebuild -workspace TravisCIDemo.xcworkspace -scheme TravisCIDemo SYMROOT="/Users/yujinhai/Desktop/GitProject/travisCIDemo"`

- Installation Build Products Location
`xcodebuild -exportArchive -archivePath build/TravisCIDemo.xcarchive -exportPath build -exportOptionsPlist export.plist`

- UITest，id是设备的UUID
`xcodebuild test -workspace MyApplication.xcworkspace -scheme iOSApp -destination 'platform=iOS,id=965058a1c30d845d0dcec81cd6b908650a0d701c'`
