---
title: Less的使用
date:  2018-2-21
tags:
- web
- 前端
- ES6
categories:
- Web
---
### let和const使用
* let用来声明变量，用法与var类似，let只在所在的代码块内有效。
```
   //let const变量的使用
    letConstFunc = () => {
        {
            let aLet = 10;
            var bVar = 20;
        }
        //not defined
        // console.log(aLet);
        console.log(bVar);
    }
```
* const声明一个只读的常量，常量的值不可修改。
```
const c=1234;
//报错
// c=234;
```
* 顶层对象的使用
   浏览器环境指的是window对象，node中是global对象。
 ```
  //可在任意位置调用
  global.c=23423;
 ```
### 变量的解构赋值
```
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
```
### 字符串的扩展
* includes 返回布尔值，表示是否找到了参数字符串
* startsWith 返回布尔值，表示参数字符串是否在原字符串的头部
* endsWith 返回布尔值，表示参数字符串是否在原字符串的尾部
```
  stringExtend = () => {
        let helloWorld="Hello World";
        // true
        console.log(helloWorld.includes("Hello"));
        //true
        console.log(helloWorld.startsWith("Hello"));
        //false
        console.log(helloWorld.endsWith("Hello"));

         // 模板字符串 ，模板字符串中可添加表达式${表达式}
                let templateStr=`
                         ${helloWorld}
                    测试
                            模板
                                     字符串
                `;
                console.log(templateStr);
    }
```
### 数值的扩展
* Number.parseInt(), Number.parseFloat()
* Math函数的使用
    * Math.trunc()去除小数部分 Math.trunc(4.1) // 4
    * ath.sign(-5) // -1 判断是正数（+1）负数（-1）还是零（0）
```
Number.parseInt('12.34') // 12
Number.parseFloat('123.45#') // 123.45
```

### 函数扩展
* 函数默认值
* 与结构默认值相结合
* rest（...变量名）参数的使用,rest参数搭配的变量是一个数组，rest参数只能作为最后一个参数。
* 函数的name属性
    * 方法的name返回方法的名称
    * 构造方法的name返回anomymous
    * bind返回的函数name属性值会加上bound前缀
    * get和set函数的name属性值前面会添加get set前缀
 * 箭头函数的使用以及作用域：定义所在的对象，而不是使用时所在的对象

```
 //函数扩展
    funcExtend=()=>{
        //输出1-----undefined
        this.funcExtendDefaultValue();
        //输出2-----3
        this.funcExtendDefaultValue(2,3);
        //解构结合使用输出1----2
        this.funcExtendDefaultValue2({y:2});
    }

    //默认值函数
    funcExtendDefaultValue=(x=1,y,...z)=>{
        console.log(x+"-----"+y);
    }

     //解构结合函数
    funcExtendDefaultValue2 = ({x = 1, y}) => {
        console.log(x + "-----" + y);
    }
```
### 数组的扩展
* 扩展运算符 （...）他好比rest函数的逆运算，将一个数组转化为用逗号分割的参数序列
* shift unshift push pop方法的使用,返回值为数组的长度
* 数组的复制
    * 直接复制，只是复制了指向数据的指针，而不是克隆全新的数组，复制的数组修改数据后会导致原数组数据发生变化
    * concat、slice函数的使用
* 数组的转换
    * Array.from();对象转数组对象
    * Array.of();一组数值转化为数组对象
* 数组方法entries，keys，values，map，forEach
```
    //数组的扩展
    arrayExtend = () => {
        //扩展运算符 1 2 3
        console.log("扩展运算符",...[1, 2, 3]);
        //方法的使用
           let array1 = [1, 2, 3];
           let array2 = [4, 5, 6];
            //push 6
            console.log("push",array1.push(...array2));
            //pop 6
            console.log("pop",array1.pop());
            //shift 1
            console.log("shift",array1.shift());
            //unshift 7
            console.log("unshift",array1.unshift(...array2));

              //直接复制
            const a1 = [1, 2];
            const a2 = a1;
            a2[0] = 2;
            a1 // [2, 2]


        //concat函数的使用,返回原数组的克隆，修改新数组数据不会影响原数组数据
            const a3 = [1, 2];
            const a4 = a2.concat();
            a4[0] = 2;
            console.log(a3) // [1, 2]

            let array11=Array.from({'0':1,'1':2,'2':3,length:3});
            //[1, 2, 3]
            console.log("111",array11);

            let array22 = Array.of(123,23423,54354);
            // [123, 23423, 54354]
            console.log("222",array22);

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
```
### 对象的扩展
* Object.is 对象比较(===)，值的严格比较
* Object.assign() 用于对象合并，浅拷贝，同名函数替换
* Object.keys()，Object.values()，Object.entries()
```
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
        console.log("object.assign",Object.assign(objectOne,{a: 1, b: 2}))
    }
```
### set和map的使用
* set类似于数组，成员的值唯一，没有重复值。
* set中add delete has clear方法的使用
* set中keys values entries foreach方法的使用
* set转化为数组的方法 [...set] , Array.from(set);
* map中get set方法的使用
```
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
```
### Class的使用
* 构造方法：使用constructor
* 使用new创建类的实例对象
* 私有方法前面添加下划线表示只限于内部使用的私有方法
* this的指向，可以使用箭头函数和bind的方法
* static静态方法的使用
* 类的继承：构造方法中出现super关键字，表示父类的构造方法
* (了解)类的 prototype 属性和__proto__属性
### Promise对象的使用
异步编程的一种解决方案。
> Promise对象是一个构造函数，用来生成Promise实例。
> Promise接受一个函数作为参数，该函数的两个参数分别为resolve（成功）和reject（失败）。
> Promise实例生成以后，可以使用then分别制定resolved和rejected状态的回调函数。
> 注意reject方法等同于抛出错误，如果在resolve后面抛出错误则抛出错误无效
>一般来说，不要在then方法里面定义 Reject 状态的回调函数（即then的第二个参数），总是使用catch方法。
> finally方法用于指定不管 Promise 对象最后状态如何，都会执行的操作

```
//unhandledRejection事件的监听函数有两个参数，第一个是错误对象，第二个是报错的 Promise 实例，它可以用来了解发生错误的环境信息
process.on('unhandledRejection', function (err, p) {
  throw err;
});
```

```
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
```