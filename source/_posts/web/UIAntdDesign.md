---
title: AntdDesign的使用
date:  2018-4-21
tags:
- web
- 前端
- AntdDesign
- Antd
categories:
- Web
---
## 安装
```
 //package.json
 npm install antd babel-plugin-import --save
 // .babelrc or babel-loader option
 {
   "plugins": [
     ["import", { "libraryName": "antd", "libraryDirectory": "es", "style": "css" }] // `style: true` 会加载 less 文件
   ]
 }
```