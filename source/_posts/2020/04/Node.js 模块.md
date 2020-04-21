---
title:   Node.js 模块
date: 2020-04-02 20:52:34
tags:
categories: nodejs
---

## Node.js 模块

- `npm init`

- `npm install <package_name>`

- 创建一个test.js文件，并require包

- 导入代码

  ```js
  exports.printMsg = function() {
    console.log("This is a message from the demo package");
  }
  ```

- 执行`node test.js`



## 注册npm账号,发布自己的代码仓库

- `npm adduser`
- `npm login`
- `npm whoami`
- `https://www.npmjs.com/~yujinhai`
- 发布到自己的仓库：`npm publish` (一定要确保自己的仓库名称唯一)
- 更新版本：`npm version <update_type>`，该命令会改变package.json文件的版本号，并且为git仓库添加tag。 然后重新发布`npm publish`

## 使用自己发布的仓库

- 创建一个文件夹：`mkdir myTest`

- `cd myTest`

- `npm init`

- `npm install <刚才上传的包>`

  





