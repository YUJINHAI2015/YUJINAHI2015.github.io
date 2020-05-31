---
title:  运行时系统结构（第三篇）
date: 2020-05-31 21:52:34
tags:
categories: 持续构建
---
### Fastlane Match



Demo: https://github.com/YUJINHAI2015/FastlaneDemo

官方文档：https://docs.fastlane.tools/actions/match/



- `fastlane init`

{% asset_img image-20200531233638653.png output %}

<img src="/Users/yujinhai/Library/Application Support/typora-user-images/image-20200531233638653.png" alt="image-20200531233638653" style="zoom:50%;" />



{% asset_img image-20200531233702698.png output %}



<img src="/Users/yujinhai/Library/Application Support/typora-user-images/image-20200531233702698.png" alt="image-20200531233702698" style="zoom:50%;" />



- `fastlane match init`

{% asset_img image-20200531234025764.png output %}



<img src="/Users/yujinhai/Library/Application Support/typora-user-images/image-20200531234025764.png" alt="image-20200531234025764" style="zoom:50%;" />

{% asset_img image-20200531234110895.png output %}



<img src="/Users/yujinhai/Library/Application Support/typora-user-images/image-20200531234110895.png" alt="image-20200531234110895" style="zoom:50%;" />

{% asset_img image-20200531234141990.png output %}



<img src="/Users/yujinhai/Library/Application Support/typora-user-images/image-20200531234141990.png" alt="image-20200531234141990" style="zoom:50%;" />



### 下载证书到git中

1、第一种：

通过 `Matchfile`

`fastlane match development` // 上传开发证书

2、第二种：

通过Fastfile

`fastlane useMatch`

{% asset_img image-20200601001331438.png output %}



<img src="/Users/yujinhai/Library/Application Support/typora-user-images/image-20200601001331438.png" alt="image-20200601001331438" style="zoom:50%;" />





### 打包

{% asset_img image-20200601001802890.png output %}



<img src="/Users/yujinhai/Library/Application Support/typora-user-images/image-20200601001802890.png" alt="image-20200601001802890" style="zoom:50%;" />



{% asset_img image-20200601001819903.png output %}



<img src="/Users/yujinhai/Library/Application Support/typora-user-images/image-20200601001819903.png" alt="image-20200601001819903" style="zoom:50%;" />





```
default_platform(:ios)

platform :ios do
  desc "Description of what the lane does"
  lane :useMatch do

	register_devices(devices_file: "./devices.txt")

	# https://docs.fastlane.tools/actions/match/
	match(
		git_url: "https://gitee.com/yujinhai/HowToUseMatch.git",
		type: "adhoc",
		#readonly: true,
		force_for_new_devices: true
	)    

	# https://docs.fastlane.tools/actions/build_app/
  	build_app(
		export_method: "ad-hoc",
	 	export_xcargs: "-allowProvisioningUpdates", 
		output_directory: "~/Desktop/outputAPI"
	)
	# https://www.pgyer.com/doc/view/fastlane
	pgyer(
		api_key: "a215682d481d742271b61aabfe1baffe", 
		user_key: "06c794bc27fbe97b626a3a21f12419f5",
		password: "123456", 
		update_description: "ss"
	)

  end
end

```









