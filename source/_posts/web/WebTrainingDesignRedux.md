---
title: Redux的使用
date:  2018-3-30
tags:
- web
- 前端
- React
- Redux
categories:
- Web
---
## 三大原则
### 1.单一数据源
#### 整个应用应用的state被存储在一个object tree中，并且这个object tree只存在于唯一的store中
### 2.State是只读的
#### 唯一改变state的方法就是触发action，action是一个用于描述已发生事件的普通对象
### 3.使用纯函数来执行修改（reducers）
#### 为了描述action如何改变state tree，你需要编写reducers。

## Action
##### Action是把数据从应用传到store的有效载荷。他是store数据的唯一来源。一般是通过store.dispatch()将action传到store。
##### Action是一个普通js对象，action内必须使用一个字符串类型的type字段来表示将要执行的动作。通常把type定义成常量，并在单独的模块进行维护。

## Reducer
##### Reducers指定了应用状态的变化如何响应actions并发送到store的。
##### Reducers就是一个纯函数，接收旧的state和action，返回新的state。
```
(previousState, action) => newState
```
##### 注意尽可能的保持reducer的纯净，不要做以下操作
* 修改传入参数
* 执行有副作用的操作，如API请求和路由跳转。
* 调用非纯函数，如Date.now()或Math.random()
