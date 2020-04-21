---
title:   Node.js 模块
date: 2020-04-02 20:52:34
tags:
categories: nodejs
---

## nodejs 模块介绍

1、Nodejs 自带服务器，不需要像其他语言要引入http服务器

2、exports 

> 把公共的功能抽离成为一个单独的js文件作为一个模块。
>
> 模块里面的`方法或者属性`是没办法访问的，要通过exports关键字
>
> 使用的时候用require(模块名称)

```js
function get() {
    console.log('get method');
}

exports.get=get;
```

```js
var obj = {
    get:function () {
        console.log('get method');
    },
    
    post:function () {
        console.log('post method');
    }
};

exports.obj=obj;
```



3、自定义的模块放到`node_modules`里面

> 默认可以通过*相对路径*找到`index.js`文件。
>
> 如果文件不是叫`index.js`，可以通过`npm init --yes` 生成描述文件。
