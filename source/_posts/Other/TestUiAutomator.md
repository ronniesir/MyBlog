---
title: 2017工作总结和计划
date: 2018-2-21
tags:
- 2018
- 工作计划
categories:
- Other
---

## UIAutomator
#### 安装
新建一个项目在gradle中添加依赖compile 
>  androidTestImplementation 'com.android.support.test.uiautomator:uiautomator-v18:2.1.2'

##### 需要注意的是minSdkVersion必须大于等于18。 
##### Android通过Annotation来识别测试用例

* 红色：通过声明@RunWith（AndroidJUnit4.class），来表示该类为一个测试集合。 
* 黄色：通过声明@Test，来表示该方法为一个测试用例。 
* 蓝色：“快进箭头”，用于运行一组测试用例。 
* 绿色：“播放箭头”，用于运行一个测试用例。

## 命令
```
adb push D:\Workspace\Android\Farmer\app\build\outputs\apk\debug\app-debug.apk /data/local/tmp/com.smart.farmer
adb shell pm install -t -r "/data/local/tmp/com.smart.farmer"

adb push D:\Workspace\Android\Farmer\app\build\outputs\apk\androidTest\debug\app-debug-androidTest.apk /data/local/tmp/com.smart.farmer.test
adb shell pm install -t -r "/data/local/tmp/com.smart.farmer.test"

adb shell am instrument -w -r   -e debug false -e class 'com.smart.farmer.ExampleInstrumentedTest#test1' com.smart.farmer.test/android.support.test.runner.AndroidJUnitRunner

```

adb shell am instrument -w -r   -e debug false -e class 'com.ronnie.testdemo.UiAutomatorTest#useAppContext' com.ronnie.testdemo.test/android.support.test.runner.AndroidJUnitRunner