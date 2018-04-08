---
title: React的使用
date:  2018-3-30
tags:
- web
- 前端
- React
categories:
- Web
---
## 基础
### 使用 create-react-app 快速构建 React 开发环境
```
$ cnpm install -g create-react-app
$ create-react-app my-app
$ cd my-app/
$ npm start
```
### 一个例子说明react的基本使用-父组件
```
import React, { Component, PureComponent } from 'react';
import './react_demo.css'
import ReactChildComponent from "./ReactChildComponent";

/**
 * 这个例子简单介绍了react的使用
 * 主要知识点包括
 * 1.component和PureComponent
 * 2.state和props初始化
 * 3.父组件向子组件中传递数据和事件
 * 4.ref的使用
 * 5.propTypes类型约束，如果类型不对会在控制台报错
 */
class ReactComponent extends Component {

    constructor(props) {
        super(props);
        //初始化state
        this.state = {
            name: "测试姓名"
        }
        this.clickMe = this.clickMe.bind(this);
    }

    clickMe = () => {
        this.setState({
            name:'你已经点击了我'
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

export default ReactComponent;
```

### 一个例子说明react的基本使用-子组件
```
import React, { PureComponent } from 'react';
import PropsType from 'prop-types';
export default class ReactChildComponent extends PureComponent {

    // 构造
    constructor(props) {
        super(props);
        // 初始状态
        this.state = {};
    }

    onChildClick = () => {
            this.props.onClickCallBack();
    }

    render() {
        return (
            <div>{this.props.name}</div>
        );
    }
}

ReactChildComponent.propTypes={
        name: PropsType.string.isRequired,
};

ReactChildComponent.defaultProps = {
      name:'默认名称'
};
```

#### prop-types包已经从react16中移除掉如果要使用需要单独安装

> npm install --save prop-types

#### 1.类型说明：
* optionalArray: React.PropTypes.array, 数组
* optionalBool: React.PropTypes.bool, 布尔类型
* optionalFunc: React.PropTypes.func, 方法
* optionalNumber: React.PropTypes.number, 数字
* optionalObject: React.PropTypes.object, 对象
* optionalString: React.PropTypes.string, 字符串
* optionalEnum: React.PropTypes.oneOf(['News', 'Photos']),限定只能接受指定值

#### 2.可以是多个对象类型中的一个
```
 optionalUnion: React.PropTypes.oneOfType([
     React.PropTypes.string,
     React.PropTypes.number,
     React.PropTypes.instanceOf(Message)
 ]),
```
#### 3.指定类型组成的数组
* optionalArrayOf: React.PropTypes.arrayOf(React.PropTypes.number),

#### 4.指定类型的属性构成的对象
* optionalObjectOf: React.PropTypes.objectOf(React.PropTypes.number),

#### 5.任意类型加上 `isRequired` 来使 prop 不可空。
* requiredFunc: React.PropTypes.func.isRequired,

#### 6.不可空的任意类型
*  requiredAny: React.PropTypes.any.isRequired,


## 更多了解 React API
### 1.setState 设置状态方法
#### setState(object nextState[, function callback])
#### 说明：
* 两个参数：第一个是新状态，新状态会和当前状态合并。第二个参数是设置成功后的回调方法，可选。
* setState方法不会立即改变this.state。所以它不是同步了，为了提高效率会批量处理执行state和dom渲染
* setState方法总会触发一次组件重绘，除非在shouldComponentUpdate中实现一些条件渲染逻辑，参考列表数据重绘逻辑。

### 2.replaceState替换状态
#### replaceState(object nextState[, function callback])
#### 说明：使用方法和setState类似，区别在于只保留新状态，原state不在新状态中的状态都会删除

### 3.setProps设置属性
#### setProps(object nextProps[, function callback])
#### 说明
* 新的props和当前的props合并

### 4.replaceProps替换属性
#### replaceProps(object nextProps[, function callback])

### 5.forceUpdate 强制刷新
####  forceUpdate([function callback])
#### 此属性适用于this.props和this.state之外的组件重绘。

### 6.获取DOM节点：findDOMNode
#### DOMElement findDOMNode()

### 7.isMounted判断组件是否挂载到dom中
#### bool isMounted()
#### 说明：返回值：true或false，表示组件是否已挂载到DOM中


## React组件生命周期
### 组件的声明周期可分成三种状态
* Mounting: 已插入真的DOM
* Updating: 正在被重新渲染
* Unmounting: 已移除真实DOM

### 生命周期的方法
* componentWillMount 渲染前调用，在客户端也在服务端
* componentDidMount 第一次渲染后滴啊用，只在客户端
* componentWillReceiveProps 在组件接收到一个新的prop时被调用，这个方法在初始化render时不会被调用。
* shouldComponentUpdate 返回一个布尔值。在组件接收到新的props或者state时被调用。在初始化时或者使用forceUpdate时不被调用。 可以在你确认不需要更新组件时使用。
* componentWillUpdate 在组件接收到新的props或state但还没render时调用，在初始化时不会调用。
* componentDidUpdate 在组件更新完成后立即调用，初始化时不会调用。
* componentWillUnmount 在组件从DOM中移除的时候立刻被调用。

### 表单中value属性和onChange时间的使用
### 在componentDidMount中获取网络数据
### React Refs的使用
```
 <input ref="myInput">
 使用this.refs.myInput获取实例
 ```
