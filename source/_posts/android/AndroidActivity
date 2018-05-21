---
title: Android Activity
date: 2018-01-13
tags:
- Activity
- IntentFilter
- Android
categories:
- Android
---

### 1. Activity生命周期

### 2. Activity启动模式

### 3. IntentFilter的匹配规则
#### IntentFilter的匹配信息有action、category、data，为了匹配过滤列表，需要同时匹配过滤列表中的action、category、data信息，否则匹配失败。
#### 一个Activity中可以有多个intent-filter，一个intent只要匹配任意一组intent-filter即可启动对应的activity
* action 的匹配要求Intent中的action存在且必须要和过滤规则中的一个action相同，action区分大小写。
* category的匹配要求Intent中如果含有category那么所有的category都必须要和过滤规则中的其中一个category相同。如果没有默认匹配'android.intent.category.DEFAULT'，所以在过滤规则最后加上这个category。
* data匹配如果过滤规则中定义了data那么Intent中必须也要定义可匹配的data。data由两部分组成mimeType和URI。
    * mimeType只媒体类型包括image/jpeg、video/*等
    * URI的结构：<schema>://<host>:<port>/[<path>|<pathPrefix>|<pathPattern>]


