---
title: fastlaneMatch
date: 2020-04-02 20:52:34
tags:
categories: 持续构建
---

## 想解决问题：1、能够自动下载最新的`profiles`文件，2、能够自动添加新的设备

## 手动管理证书
1、在苹果开发中心，下载 `certificate (.cer) `，并安装到本地
2、下载`provisioning profile (.mobileprovision)`，并安装到本地
3、勾选Xcode里面的Automatic选项，然后打包。


## 使用`match`管理证书
1、私有git仓库存储：` private keys ` 和 `certificates`
2、换新电脑或者多人的项目比较实用

## 使用`cert`和`sigh`管理证书
```
lane :beta do
  get_certificates           # 自动下载，要输入苹果账号
  get_provisioning_profile   # 自动下载，要输入苹果账号
  build_app
end

```

## 下面重点介绍 `match` 方法管理证书

1、`match` 插件会自动下载`certificates & provisioning profiles`
2、会自动修复过期或损坏的`certificates & provisioning profiles`
3、通过git仓库方式管理，很方便团队之间的合作
4、手动管理git和通过`match`管理的差别。[参考链接](https://codesigning.guide)
5、手动管理，会有各种证书过期，和各种证书副本问题


## 初始化match
1、`fastlane match init` 输入存储证书的git仓库
2、`fastlane match development` 自动生成并上传证书（adhoc, development, appstore, enterprise）

- 输入密码，并且保存到keychain里面 [passphrase](https://docs.fastlane.tools/actions/match/#passphrase)
- `~/Library/MobileDevice/Provisioning Profiles` 可以查看到安装的文件

3、在新电脑拉取证书

- `fastlane match development` // 会通过苹果管理中心拉取最新证书
- `fastlane match development --readonly` // 不会更新证书

## 访问控制--证书同步和分发问题
1、通过`match`命令存储证书到git上面
2、其他开发者通过密码可以访问git仓库
3、其他开发者通过`match`命令就可以在git仓库获取到最新的证书，并且不能访问苹果中心
4、当我们自己更像git仓库是，能够确保其他开发者通过`match`获取到最新的证书
5、只能通过`fastlane match development --readonly` 方式访问，这样才不用通过苹果中心拉取。


## 当前需要解决的问题
1、访问git的权限
2、获取到证书后，解码的问题

## 持续构建

https://docs.fastlane.tools/actions/match/#passphrase

https://docs.fastlane.tools/best-practices/continuous-integration/travis/

https://docs.fastlane.tools/getting-started/ios/setup/#use-a-gemfile

https://docs.fastlane.tools/#metrics    

