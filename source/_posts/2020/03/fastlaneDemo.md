---

title: fastlane
date: 2020-03-21 22:25:59
categories: 持续构建

---

## [demo 地址](https://github.com/YUJINHAI2015/FastlaneDemo/tree/master/FastlaneDemo)

## 安装：[官网](https://docs.fastlane.tools/getting-started/ios/setup/)
- 查看是否安装成功：`fastlane --version`

## 简单使用
- 用`xcode`新建项目`FastlaneDemo`
- 用命令行进入到`FastlaneDemo`所在的路径，创建一个文件夹和两个空文件，运行下面命令：

```
$: mkdir fastlane
$: touch fastlane/Appfile
$: touch fastlane/Fastfile

```
- 在`Fastfile`文件里面输入这段语句：

- `open fastlane/Fastfile `
```
lane :OutputHelloWorld do
  puts "helloWorld"
end

```
- 在命令行中运行 `fastlane OutputHelloWorld`

{% asset_img OutputHelloWorld.png output %}

- [常用参数列表](https://docs.fastlane.tools/actions/run_tests/#parameters)
