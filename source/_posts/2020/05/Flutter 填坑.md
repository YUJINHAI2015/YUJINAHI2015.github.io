---
title: fastlaneMatch
date: 2020-05-02 20:52:34
tags:
categories: Flutter
---
### Flutter 填坑

>  Error connecting to the service protocol: failed to connect to http://127.0.0.1:1024
>
> 解决办法，手机和电脑连接在同一个网络



> ### 
>
> ```js
> error: Building for iOS, but the linked and embedded framework 'App.framework' was built for iOS Simulator. (in target 'Runner' from
> project 'Runner')
> ```
>
> [解决办法](https://github.com/flutter/flutter/issues/50568)
>
> `rm -rf ios/Flutter/App.framework`

