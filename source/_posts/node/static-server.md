---
title: 快速搭建静态页面服务器
date: 2017/2/13 22:35:26
tags: [Node,服务器]
categories: 前端
---

### 静态文件
静态文件一般指js,css,html，图片视频,还有一些供人下载的文件之类，不涉及、后台、数据库等操作，那么如何用Node.js框架快速搭建静态页面服务器呢

<!-- more -->
### **Express**
```js
    var express = require("express");
    var app = express();
    var port = 8080;
    app.use(express.static(__dirname + "/", {index: "index.html"}));
    app.listen(port);
    console.log('httpServer at http://localhost:' + port);

```
### **Koa**+**koa-static**
```js
    var serve = require('koa-static');
    var koa = require('koa');
    var app = koa();
    var port = 8080;
    app.use(serve('.', {index: "index.html"})); //默认为index.html
    app.listen(port);
    console.log('httpServer at http://localhost:' + port);
```

