---
title: Router4的使用
date:  2018-4-3
tags:
- web
- 前端
- React
- Router
categories:
- Web
---
```
npm install --save react-router-dom
```
## 组件
### <BrowserRouter>
##### 一个高阶路由组件，保证你的UI界面和URL保持同步。
#### 1. basename:string
##### 作用：为所有位置添加一个基准URL
##### 使用场景：加入你把页面部署到服务器的二级目录下，你可以使用basename设置此目录
```
<BrowserRouter basename="/minooo" />
<Link to="/react" /> // 最终渲染为 <a href="/minooo/react">
```
#### 2. getUserConfirmation: func
##### 导航到此页面前执行的函数
```
<BrowserRouter getUserConfirmation={getConfirmation('Are you sure?', yourCallBack)} />
```
#### 3. forceRefresh: bool
##### 当浏览器不支持 HTML5 的 history API 时强制刷新页面。
#### 4. keyLength: number
##### 作用：设置它里面路由的 location.key 的长度。默认是6。（key的作用：点击同一个链接时，每次该路由下的 location.key都会改变，可以通过 key 的变化来刷新页面。）
#### 5. children: node
##### 作用：渲染唯一子元素。

### <HashRouter>
##### 不支持 location.key 和 location.state。另外由于该技术只是用来支持旧版浏览器，因此更推荐大家使用 BrowserRouter

### <Route>
##### 最重要的组件,自带三个 render method 和三个 props
#### render method
##### 每种 render method 都有不同的应用场景，同一个<Route> 应该只使用一种 render method ，大部分情况下你将使用 component

##### 1.\<Route component>
##### 只有当访问地址和路由匹配时，一个 React component 才会被渲染，此时此组件接受 route props (match, location, history)。
```
<Route path="/user/:username" component={User} />
const User = ({ match }) => {
  return <h1>Hello {match.params.username}!</h1>
}
```
##### 2.\<Route render> func
##### 此方法适用于内联渲染，而且不会产生上文说的重复装载问题。
```
<Route path="/home" render={() => <h1>Home</h1} />
```

##### 3.\<Route children>
##### 4.path:string
##### 任何可以被 path-to-regexp解析的有效 URL 路径,如果不设置path路由将总是匹配
```
<Route path="/users/:id" component={User} />
```
##### 5.exact: bool
##### 如果为 true，path 为 '/one' 的路由将不能匹配 '/one/two'，反之，亦然。
##### 6.strict: bool
##### 对路径末尾斜杠的匹配。如果为 true。path 为 '/one/' 将不能匹配 '/one' 但可以匹配 '/one/two'。
##### 如果要确保路由没有末尾斜杠，那么 strict 和exact 都必须同时为 true
#### props

### \<Link> 提供声明式导航
##### to: string 作用：跳转到指定路径
```
<Link to="/courses" />
```
##### to: object 作用：携带参数跳转到指定路径
```
<Link to={{
  pathname: '/course',
  search: '?sort=name',
  state: { price: 18 }
}} />
```
### \<NavLink> link的特殊，为页面导航准备的因为导航需要有激活状态
##### activeClassName: string
##### 导航选中激活时候应用的样式名，默认样式名为 active
```
<NavLink
  to="/about"
  activeClassName="selected"
>MyBlog</NavLink>
```
###### activeStyle: object 如果不想使用上面样式名可以直接使用这个属性写样式
```
<NavLink
  to="/about"
  activeStyle={{ color: 'green', fontWeight: 'bold' }}
>MyBlog</NavLink>
```
##### exact: bool
##### 若为 true，只有当访问地址严格匹配时激活样式才会应用
##### strict: bool
##### 若为 true，只有当访问地址后缀斜杠严格匹配（有或无）时激活样式才会应用
##### isActive: func
##### 决定导航是否激活，或者在导航激活时候做点别的事情。不管怎样，它不能决定对应页面是否可以渲染。

### \<Switch>
##### 只渲染出第一个与当前访问地址匹配的 \<Route> 或 \<Redirect>。
### \<Redirect>
##### 渲染时将导航到一个新地址，这个新地址覆盖在访问历史信息里面的本该访问的那个地址。
##### to: string
##### 重定向的 URL 字符串
##### to: object
##### 重定向的 location 对象
##### push: bool
##### 若为真，重定向操作将会把新地址加入到访问历史记录里面，并且无法回退到前面的页面。
##### from: string
##### 需要匹配的将要被重定向路径。
### Prompt 当用户离开当前页面前做出一些提示。
message: string
当用户离开当前页面时，设置的提示信息。
```
<Prompt message="确定要离开？" />
```
message: func
当用户离开当前页面时，设置的回掉函数
```
<Prompt message={location => (
  `Are you sue you want to go to ${location.pathname}?`
)} />
```
when: bool
通过设置一定条件要决定是否启用 Prompt
```
<Prompt
          when={this.state.dirty}
          message="数据尚未保存，确定离开？" />
```
### 对象和方法
##### history对会话历史的管理
```
我们会经常使用以下术语：
"browser history" - history 在 DOM 上的实现，用于支持 HTML5 history API 的浏览器
"hash history" - history 在 DOM 上的实现，用于旧版浏览器。
"memory history" - history 在内存上的实现，用于测试或非 DOM 环境（例如 React Native）。
history 对象通常具有以下属性和方法：

length: number 浏览历史堆栈中的条目数
action: string 路由跳转到当前页面执行的动作，分为 PUSH, REPLACE, POP
location: object 当前访问地址信息组成的对象，具有如下属性：
pathname: string URL路径
search: string URL中的查询字符串
hash: string URL的 hash 片段
state: string 例如执行 push(path, state) 操作时，location 的 state 将被提供到堆栈信息里，state 只有在 browser 和 memory history 有效。
push(path, [state]) 在历史堆栈信息里加入一个新条目。
replace(path, [state]) 在历史堆栈信息里替换掉当前的条目
go(n) 将 history 堆栈中的指针向前移动 n。
goBack() 等同于 go(-1)
goForward 等同于 go(1)
block(prompt) 阻止跳转
```
##### 注意：history是可变的，因此建议从route的prop中获取location，而不是从history.location直接获取。
```
 componentWillReceiveProps(nextProps) {
    // locationChanged
    const locationChanged = nextProps.location !== this.props.location
    // 错误方式，locationChanged 永远为 false，因为history 是可变的
    const locationChanged = nextProps.history.location !== this.props.history.location
  }
```
### location是指你当前的位置
```
{
  key: '123'
  pathname: '/about',
  search: '?name=123'
  hash: '#123',
  state: {
    price: 324234
  }
}
```
#### 在以下情境中可以获取 location 对象
* 在 Route component 中，以 this.props.location 获取
* 在 Route render 中，以 ({location}) => () 方式获取
* 在 Route children 中，以 ({location}) => () 方式获取
* 在 withRouter 中，以 this.props.location 的方式获取
### match
#### 包含了Route path如何与URL匹配的信息
##### 包含属性如下：
* params: object 路径参数，通过解析 URL 中的动态部分获得键值对
* isExact: bool 为 true 时，整个 URL 都需要匹配
* path: string 用来匹配的路径模式，用于创建嵌套的 <Route>
* url: string URL 匹配的部分，用于嵌套的 <Link>
##### 在以下情境中可以获取 match 对象
* 在 Route component 中，以 this.props.match获取
* 在 Route render 中，以 ({match}) => () 方式获取
* 在 Route children 中，以 ({match}) => () 方式获取
* 在 withRouter 中，以 this.props.match的方式获取
* matchPath 的返回值

## 相关链接
[React-Router4.x中文文档](https://www.cnblogs.com/zhanghuiming/p/7592132.html)
[React Router](https://reacttraining.com/react-router/web/example/basic)
<!-- [初探 React Router 4.0](https://blog.csdn.net/sinat_17775997/article/details/69218382) -->