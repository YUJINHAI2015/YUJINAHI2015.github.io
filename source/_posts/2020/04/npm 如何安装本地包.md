---
title:   npm 安装并管理版本
date: 2020-04-02 20:52:34
tags:
categories: nodejs
---

## npm 安装并管理版本

- 如果是作为命令行工具使用，就安装全局包
- 安装本地包：`npm install <package_name>`
- 安装全局包：`npm install -g <package_name>`
- 更新包：`npm update /-g <package_name>`
- 卸载包：`npm uninstall /-g <package_name>`

## 进阶

- 默认安装全部依赖：`npm install` 
- 生产环境：`npm install <package_name> --save`
- 开发环境：`npm install <package_name> --save-dev`

- 直接安装git连接地址：`npm install <git remote url>`

- 用@指定版本：`npm install sax@1.0.0` `npm install sax@">=0.1.0<0.2.0"`

- 不触发脚本：`npm install sax --ignore-scripts`



```
"dependencies": {
  "md5": "^2.2.1" 
}

```
> `^` 表示第一位版本号不变，后面两位取最新
> `~` 表示前面两位不变，最后一个取最新
> `*` 表示全部取最新
