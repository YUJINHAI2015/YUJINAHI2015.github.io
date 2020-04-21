---
title:  Express 应用程序生成器
date: 2020-04-02 20:52:34
tags:
categories: nodejs
---

# Express 应用程序生成器

[Express](https://www.expressjs.com.cn/starter/generator.html)

- `sudo npm install -g express-generator`



> express -h 
>
> `zsh: command not found: express`
>
> 1、`open ~/.bash_profile `
>
> 2、添加`export PATH=$PATH:$HOME/.npm-global/bin:$PATH` 
>
> 3、`source ~/.bash_profile `
>
> 4、查看是否添加成功`echo $PATH`
>
> 5、`express -h`



## 生成模板

1、`express --view-pug myapp`

2、`cd myapp`

3、`npm install`

4、`DEBUG=myapp:* npm start`

