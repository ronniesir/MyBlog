---
title: Vue-router的使用
date:  2018-2-21
tags:
- web
- 前端
- vue-router
categories:
- Web
---
#### 基础
```HTML
<!-- 使用 router-link 组件来导航. -->
<router-link to="/foo">Go to Foo</router-link>
<!-- 路由出口 -->
<!-- 路由匹配到的组件将渲染在这里 -->
<router-view></router-view>
```
我们可以在任何组件内通过 this.$router 访问路由器
```HTML
<!-- 路由传参数 -->
{ path: '/user/:id', component: User }
<!-- 路由获取参数 -->
this.$route.params.id
```
#### 响应路由参数的变化
```HTML
 watch: {
    '$route' (to, from) {
      // 对路由变化作出响应...
    }
  }

   beforeRouteUpdate (to, from, next) {
    // react to route changes...
    // don't forget to call next()
  }
```
