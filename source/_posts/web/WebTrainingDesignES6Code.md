---
title: ES6培训用例代码
date:  2018-3-29
tags:
- web
- 前端
- ES6
categories:
- Web
---
```
import React, { Component } from 'react';

class Home extends Component {

    // 构造
    constructor(props) {
        super(props);
        // 初始状态
        this.state = {};
    }

    componentDidMount() {
        //let和const的学习
        this.letConstFunc();
        this.variableDeconstruction();
        this.stringExtend();
        this.numberExtend();
        this.funcExtend();
        this.arrayExtend();
        this.objectExtend();
        this.mapSet();
        this.promiseUse();
    }


    /**
     * let const变量的使用
     */
    letConstFunc = () => {
        {
            let aLet = 10;
            var bVar = 20;
        }
        //not defined
        // console.log(aLet);
        console.log(bVar);

        const c = 1234;
        //报错
        // c=234;

        //可在任意位置调用
        global.c = 23423;
    }

    /**
     * 变量的解构赋值
     */
    variableDeconstruction = () => {
        //数组解构
        let [aa, bb, cc] = [11, 22, 33];
        //11-22-33
        console.log(aa + "-" + bb + "-" + cc);

        //对象解构
        let {o1, o2} = {o1: 1, o2: 2};
        //1-2
        console.log(o1 + "-" + o2);
    }

    //字符串扩展
    stringExtend = () => {
        let helloWorld = "Hello World";
        // true
        console.log(helloWorld.includes("Hello"));
        //true
        console.log(helloWorld.startsWith("Hello"));
        //false
        console.log(helloWorld.endsWith("Hello"));

        // 模板字符串
        let templateStr = `
            ${helloWorld}
            测试
                    模板
                             字符串
        `;
        console.log(templateStr);
    }

    //数值扩展
    numberExtend = () => {
        let intData = Number.parseInt('12.34') // 12
        let floatData = Number.parseFloat('123.45#') // 123.45
        let truncData = Math.trunc(4.1);
        //12---123.45---4
        console.log(intData + "---" + floatData + "---" + truncData);
    }

    //函数扩展
    funcExtend = () => {
        //输出1-----undefined
        this.funcExtendDefaultValue();
        //输出2-----3
        this.funcExtendDefaultValue(2, 3);
        this.funcExtendDefaultValue2({y: 2});
    }

    //默认值函数
    funcExtendDefaultValue = (x = 1, y, ...values) => {
        console.log(x + "-----" + y);
    }

    //解构结合函数
    funcExtendDefaultValue2 = ({x = 1, y}) => {
        console.log(x + "-----" + y);
    }

    //数组的扩展
    arrayExtend = () => {
        //扩展运算符 1 2 3
        console.log("扩展运算符", ...[1, 2, 3]);

        let array1 = [1, 2, 3];
        let array2 = [4, 5, 6];
        console.log("push", array1.push(...array2));
        console.log("pop", array1.pop());
        console.log("shift", array1.shift());
        console.log("unshift", array1.unshift(...array2));

        //直接复制
        const a1 = [1, 2];
        const a2 = a1;
        a2[0] = 2;
        console.log(a1) // [2, 2]

        //concat函数的使用,返回原数组的克隆，修改新数组数据不会影响原数组数据
        const a3 = [1, 2];
        const a4 = a2.concat();
        a4[0] = 2;
        console.log(a3) // [1, 2]

        let array11 = Array.from({'0': 1, '1': 2, '2': 3, length: 3});
        //[1, 2, 3]
        console.log("111", array11);

        let array22 = Array.of(123, 23423, 54354);
        // [123, 23423, 54354]
        console.log("222", array22);

        // 0
        // 1
        for (let index of ['a', 'b'].keys()) {
            console.log(index);
        }

        // 0 "a"
        // 1 "b"
        for (let [index, elem] of ['a', 'b'].entries()) {
            console.log(index, elem);
        }

    }

    //对象的扩展
    objectExtend = () => {
        const objectKey = 'objectValue';
        const objectNew = {objectKey};
        //{objectKey: "objectValue"}
        console.log("obejct new", objectNew);

        //属性名表达式
        //{objectKey: "objectValue", abc: "abd"}
        objectNew['a' + 'bc'] = 'abd';
        console.log("obejct new", objectNew);

        let objectOne = {};
        //返回false 两个不同的对象
        console.log("object.is", Object.is({}, {}));
        //{a: 1, b: 2}
        console.log("object.assign", Object.assign(objectOne, {a: 1, b: 2}))
    }

    //set和map的使用
    mapSet = () => {
        const set = new Set([11, 22, 33, 4, 5, 6, 123, 11, 22, 33, 4]);

        set.add(456);
        //11 22 33 4 5 6 123 456
        set.forEach((item) => {
            console.log(item);
        });

        const map = new Map();
        map.set("name", "value");
        console.log("map",map.get("name"));
        map.has("name");
        map.delete("name");
    }

    //promise的使用
    promiseUse=()=>{

        const promiseSuccess = new Promise((resolve,reject)=>{
            resolve("成功了");
            throw new Error("成功后抛出无效");
        })

        //成功处理
        promiseSuccess.then((successValue)=>{
            console.log(successValue)
        }).catch((failedValue)=>{
            console.log("error",failedValue)
        });

        const promiseFailed = new Promise((resolve,reject)=>{
            reject(new Error('失败后抛出'));

        })

        //失败调用直接在catch中进行处理
        promiseFailed.then((successValue)=>{

        }).catch((error)=>{
            console.log("error",error)
        }).finally(()=>{
            console.log("finally")
        });


    }



    render() {
        return (
            <div>
                <h2>Home Page</h2>
                <p>Home Page Content</p>
            </div>
        );
    }
}

Home.propTypes = {};
Home.defaultProps = {};

export default Home;
```