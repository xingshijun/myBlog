---
title: node服务安装和部署
date: 2019-06-18 11:22:35
tags: node express
categories: Node
---
### 部署环境
<!-- more -->
```
npm install express --save -g
npm install express-generator --save -g
express projectname //创建项目目录
cd projectname //进入项目
npm install //安装依赖
npm start //开启服务

bin: 用于应用启动，可在里面设置启动的端口号等。

/public: 静态资源目录

/routes：可以认为是controller（控制器）目录，路由。

/views: jade模板目录，可以认为是view(视图)目录
```
### 利用 Express 托管静态文件
```
app.use(express.static('public'))
app.use('/static', express.static(path.join(__dirname, 'public')))
```
