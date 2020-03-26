---
title: fastlane自动化打包
date: 2020-03-27 00:26:40
tags:
categories: 持续构建
---
## [参考蒲公英地址](https://www.pgyer.com/doc/view/fastlane)
## [参考地址](https://www.jianshu.com/p/43b703b6eb45)

## (demo地址)[]

## 定义lane
```
lane :archive do

  puts "请输入版本描述信息："
  desc = STDIN.gets

  build_app(export_method: "ad-hoc", output_directory: "ipa")
  pgyer(api_key: "a215682d481d742271b61aabfe1baffe", user_key: "06c794bc27fbe97b626a3a21f12419f5",password: "12345678", update_description: "#{desc}")
  
end
```

## 遇到问题，

1 、fastlane 版本太低，
`sudo gem install fastlane`

2、项目需要指定 `team`
