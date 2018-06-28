---
title: Vue的使用
date:  2018-6-21
tags:
- web
- 前端
- Vue
categories:
- Web
---
## Vue学习笔记
#### 使用vue-cli构建项目
1. 安装vue-cli
    > npm install -g vue-cli

2. 使用vue-cli构建项目（建议关闭ESLint检查）
    > vue init webpack VueDemo(项目名称)

#### vue语法学习

#### 1. 数据

当vue实例创建的时，它向vue中加入了其data对象中所能找到的属性。当这些属性值发生变化的时候，视图会更新。注意只有当实例对象创建时data中存在的属性才是响应式的，新增属性的改变不会触发视图的更新。
```HTML
var data ={a:1}
var vm = new Vue({
    data:data
})
vm.a=2;//data.a等于2
vm.b=3;//新增属性不会触发页面更新
```
##### 注意：使用 Object.freeze()，这会阻止修改现有的属性，也意味着响应系统无法再追踪变化。 Vue 实例还暴露了一些有用的实例属性与方法。它们都有前缀 $

#### 2. 实例生命周期
生命周期钩子的this上下文指向调用它的Vue实例，不要在选项属性和回调上使用箭头函数，因为箭头函数和父级上下文绑定，在箭头函数中使用this经常会导致回去不到vue实例

* beforeCreate
* created 实例创建后调用
* beforeMount
* mounted
* beforeUpdate
* updated
* beforeDestroy
* destroyed

#### 3.模板语法
* 使用“Mustache”语法 (双大括号) 的文本插值
* 通过使用 v-once 指令，你也能执行一次性地插值，当数据改变时，插值处的内容不会更新
* 双大括号会将数据解释为普通文本，而非 HTML 代码。为了输出真正的 HTML，你需要使用 v-html 指令
* 指令 (Directives) 是带有 v- 前缀的特殊特性
    * v-hind
    * v-on
    * v-if
    * v-for
* 修饰符：修饰符 (Modifiers) 是以半角句号 . 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定
* 缩写
    * v-bind缩写
    ```HTML
    <!-- 完整语法 -->
    <a v-bind:href="url">...</a>

    <!-- 缩写 -->
    <a :href="url">...</a>
    ```
    * v-on缩写
    ```HTML
    <!-- 完整语法 -->
    <a v-on:click="doSomething">...</a>
    <!-- 缩写 -->
    <a @click="doSomething">...</a>
    ```
#### 4.计算属性
对于任何复杂逻辑，你都应当使用计算属性.计算属性是基于它们的依赖进行缓存的。计算属性只有在它的相关依赖发生改变时才会重新求值。这就意味着只要 message 还没有发生改变，多次访问 reversedMessage 计算属性会立即返回之前的计算结果，而不必再次执行函数.
#### 5.Class与Style绑定
* 对象语法 
```HTML
<div v-bind:class="{ active: isActive }"></div>
```
* 数组语法
```HTML
<div v-bind:class="[activeClass, errorClass]"></div>
```
* 绑定内联样式
```HTML
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>

<div v-bind:style="styleObject"></div>

<div v-bind:style="[baseStyles, overridingStyles]"></div>
```
#### 6. 条件渲染
* v-if()
    ```HTML
    <h1 v-if="ok">Yes</h1>
    <h1 v-else>No</h1>
    ```
v-else 元素必须紧跟在带 v-if 或者 v-else-if 的元素的后面，否则它将不会被识别。

* 用key管理复用的元素
    ```HTML
    v-show 不支持 <template> 元素，也不支持 v-else。
    ```

* v-show 只是样式上切换view的显示。
* v-for 根据数据遍历当前元素,在 v-for 块中，我们拥有对父作用域属性的完全访问权限。
    ```HTML
    <ul id="example-1">
    <li v-for="（item,index) in items">
        {{ item.message }}
    </li>
    </ul>
    ```
    你也可以用 of 替代 in 作为分隔符
    ```HTML
    <div v-for="item of items"></div>
    ```
* 对象的 v-for属性
```HTML
<ul id="v-for-object" class="demo">
  <li v-for="value in object">
    {{ value }}
  </li>
</ul>

new Vue({
  el: '#v-for-object',
  data: {
    object: {
      firstName: 'John',
      lastName: 'Doe',
      age: 30
    }
  }
})
```
你也可以第二个参数为键名第三个参数为索引
```HTML
<div v-for="(value, key, index) in object" v-bind:key="item.id">
  {{ index }}. {{ key }}: {{ value }}
</div>
```

在遍历对象时，是按 Object.keys() 的结果遍历，但是不能保证它的结果在不同的 JavaScript 引擎下是一致的。

* 变异方法会改变原始数组
    * push
    * pop
    * shift
    * unshift
    * splice
    * sort
    * reverse
* 非变异方法
    * filter
    * concat
    * slice()

    这些不会改变原始数组，但总是返回一个新数组
##### 注意1：利用索引直接设置一项或修改数组长度不会触发状态更新
##### 解决方法：
* vm.$set(vm.items, indexOfItem, newValue)
* vm.items.splice(indexOfItem, 1, newValue)
* vm.items.splice(newLength)
##### 注意2：Vue 不能检测对象属性的添加或删除
##### 解决方法：Vue.set(object, key, value)
```HTML
Vue.set(vm.userProfile, 'age', 27)
vm.$set(vm.userProfile, 'age', 27)
```
##### 有时你可能需要为已有对象赋予多个新属性在这种情况下，你应该用两个对象的属性创建一个新的对象。所以，如果你想添加新的响应式属性，不要像这样：
```HTML
Object.assign(vm.userProfile, {
  age: 27,
  favoriteColor: 'Vue Green'
})
```
你应该：
```HTML
vm.userProfile = Object.assign({}, vm.userProfile, {
  age: 27,
  favoriteColor: 'Vue Green'
})
```
#### 7. 事件处理
  * 事件修饰符（v-on提供了事件修饰符）
    * .stop 阻止单击事件继续传播
    * .prevent 提交事件不再重载页面
    * .capture 添加事件监听器时使用事件捕获模式，即元素自身触发的事件先在此处处理，然后才交由内部元素进行处理
    * .self 只当在 event.target 是当前元素自身时触发处理函数
    * .once 只执行一次
    * .passive
  * 按键修饰符
    * .enter
    * .tab
    * .delete (捕获“删除”和“退格”键)
    * .esc
    * .space
    * .up
    * .down
    * .left
    * .right
    ```HTML
    <input v-on:keyup.enter="submit">
    ```
#### 8. 表单输入绑定
##### 你可以用 v-model 指令在表单 \<input> 及 \<textarea> 元素上创建双向数据绑定
* .lazy 在change时而非input时更新
* .number 自动将用户输入值转为数值类型。
* .trim 自动过滤用户输入的首尾空白字符。
#### 9. 组件基础
    因为组件是可复用的 Vue 实例，所以它们与 new Vue 接收相同的选项，例如 data、computed、watch、methods 以及生命周期钩子等。仅有的例外是像 el 这样根实例特有的选项。

* 父组件向子组件传值。
```HTML
<blog-post
      v-for="post in posts"
      v-bind:key="post.id"
      v-bind:post="post"
    ></blog-post>
<!-- 子组件接收 -->
Vue.component('blog-post', {
  props: ['post'],
  template: `
    <div class="blog-post">
      <h3>{{ post.title }}</h3>
      <div v-html="post.content"></div>
    </div>
  `
})
```

* 通过事件向父级组件发送消息

    ##### 我们可以调用内建的 $emit 方法并传入事件的名字，来向父级组件触发一个事件
    ```HTML
    <button v-on:click="$emit('enlarge-text')">
    Enlarge text
    </button>
    <!-- 向父组件传值 -->
    <button v-on:click="$emit('enlarge-text', 0.1)">
    Enlarge text
    </button>
    <!-- 父组件通过 $event 访问到被抛出的这个值-->
    <blog-post v-on:enlarge-text="postFontSize +=$event"></blog-post>

    <!-- 如果事件处理函数是一个方法 -->
    <blog-post v-on:enlarge-text="onEnlargeText"></blog-post>
    <!-- 那么这个值将作为第一个参数传入到这个方法 -->
    methods: {
        onEnlargeText: function (enlargeAmount) {
            this.postFontSize += enlargeAmount
        }
    }
    ```
#### 10. 深入了解组件
* 组件的注册
    * 全局注册
    ```HTML
    Vue.component('my-component-name', {
    })
    ```
    * 局部注册
    ```HTML
    var ComponentA = { /* ... */ }
    new Vue({
        el: '#app'
        components: {
        'component-a': ComponentA,
        }
    })
    ```
* 传递静态或动态props
```HTML
<blog-post title="My journey with Vue"></blog-post>
<blog-post v-bind:title="post.title"></blog-post>
```
* props type验证



#### 参考资料
1. [Vue中文文档](https://cn.vuejs.org/v2/guide/instance.html)