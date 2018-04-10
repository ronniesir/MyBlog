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
### [Redux中文文档](http://www.redux.org.cn/)
# 最简单的实例
##### 如果你不确定是否需要它，那么其实你是不需要它的，当你遇到问题才使用redux。
```
 npm install --save redux
 npm install --save react-redux
```
### 步骤
#### 1.创建store并使用provider传递store到所有组件
```
import thunk from 'redux-thunk'
import indexReducers from './reducers';
import { Provider } from 'react-redux';
import { createStore, applyMiddleware } from 'redux';
//createStore所创建的redux store没有middleware所以只支持同步数据流
//可以使用applyMiddleware来增强createStore。
const store = createStore(indexReducers, applyMiddleware(thunk));
ReactDOM.render((
    <Provider store={store}>
        <BrowserRouter>
            <ReactComponent/>
        </BrowserRouter>
    </Provider>
), document.getElementById('root'))
```
#### 2.定义个Action创建函数
```
export function testAction(){
    return {
        type:'TEST_ACTION',
        text:'测试数据'
    }
}
```
#### 3.创建reducer并组合
```
//文件 TestReducer.js
const testFun = (state = [], action) => {

    switch (action.type) {
        case 'TEST_ACTION':
            return Object.assign({}, state, {text:action.text})
        default :
            return state;
    }
}
export default testFun;


//reducer下的index文件进行组合
import { combineReducers } from 'redux';
//此处名称决定了引用变量的名称
import TestReducer from './TestReducer';

const ReducerIndex = combineReducers({
    TestReducer
})

export default ReducerIndex;
```
#### 4.展示页面调用
```
class ReactComponent extends Component {

    constructor(props) {
        super(props);
        //初始化state
        this.state = {
            name: "测试姓名"
        }
        this.clickMe = this.clickMe.bind(this);
    }

    componentDidMount() {

    }

    componentWillReceiveProps(props) {
        this.setState({
            name: props.name
        })
    }


    clickMe = () => {
        this.props.dispatch({
            type:'TEST_ACTION',
            text:'点击返回了数据-测试'
        })
    }

    render() {
        return (
            <div className="bgContainer">

                {/*ref使用和state中参数的使用，向子组件中传递数据和事件*/}
                <ReactChildComponent
                    ref={(childClick) => {
                        this.childClick = childClick
                    }}
                    name={this.state.name}
                    onClickCallBack={() => {
                        this.clickMe();
                    }}
                />

                {/*点击通过ref获取子控件触发子控件中的方法*/}
                <div
                    onClick={() => {
                        this.childClick.onChildClick();
                    }}>
                    ref to click
                </div>

            </div>
        )
    }

}

const mapDispatchToProps = (state) => {
    //此处TestReducer名称和reducer引入名称有关
    return {
        name: state.TestReducer.text
    }
}

export default connect(mapDispatchToProps)(ReactComponent);
```
# 理论
## 三大原则
##### 严格的单向数据流是Redux架构的设计核心
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

##### combineReducers所做的只是生成一个函数，这个函数来调用你的一些列reducer，每个reducer根据他们的key来筛选出state中的一部分数据并出来，然后这个生成函数在将所有reducer的结果合并成一个大的对象。


## Store
### Store职责
* 维持应用的 state；
* 提供 getState() 方法获取 state；
* 提供 dispatch(action) 方法更新 state；
* 通过 subscribe(listener) 注册监听器;
* 通过 subscribe(listener) 返回的函数注销监听器。
##### 强调Redux应用只有一个单一的store，当拆分数据处理逻辑时，你应该使用reducer组合而不是创建多个store。
```
//创建一个store 如果是多个reducer可以使用combineReducers()方法合并
//createStore第二个参数是可选的用来设置state初始化状态
let store = createStore(reducers);
// 注意 subscribe() 返回一个函数用来注销监听器
const unsubscribe = store.subscribe(() =>
  console.log(store.getState())
)
// 停止监听 state 更新
unsubscribe();
```

# 高级（可后期了解）
## 异步Action
#### 一般情况下，每个API请求都需要dispatch至少三种action
* 一种通知 reducer 请求开始的 action。开始loading
* 一种通知 reducer 请求成功的 action。隐藏loading，显示数据
* 一种通知 reducer 请求失败的 action。隐藏loading，提示失败信息
个人喜欢定义不同的type展示
```
{ type: 'FETCH_POSTS_REQUEST' }
{ type: 'FETCH_POSTS_FAILURE', error: 'Oops' }
{ type: 'FETCH_POSTS_SUCCESS', response: { ... } }
```
#### 异步action创建函数
##### action创建函数除了返回action对象还可以返回函数，这是action创建函数就成为了thunk。当action创建函数返回函数时，这个函数会被Redux Thunk middleware执行。
```
//定义个异步的action创建函数
export  function fetchDataAction(){
    return function(dispatch){
        return fetch('url')
                .then((success)=>{})
    }
}
//调用,thunk的一个优点就是它的结果可以再次被dispatch
store.dispatch(fetchDataAction());
```
## Middleware中间件
##### 它提供的是位于 action 被发起之后，到达 reducer 之前的扩展点
```
indexReducers, applyMiddleware(thunk,...);
```

## 最常见的问题
#### 为什么组件没有被重新渲染，或则mapStateToProps没有运行
##### 最常见的原因就是对state进行了直接的修改，redux期望reducer以不可变的方式更新state。如果直接返回同一个对象，redux也会认为没有变化。