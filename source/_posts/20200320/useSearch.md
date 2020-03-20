---
title: useSearch
date: 2020-03-20 23:12:09
categories: hexo
---
1、`npm install hexo-generator-searchdb --save`
2、在主题`_config.yml` 添加
```
search:
path: search.xml
field: post
format: html
limit: 10000

```
3、找到这个
```
# Local search
local_search:
  enable: true
  
```
