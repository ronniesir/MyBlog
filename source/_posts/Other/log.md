---
title: 每日做的事情
date: 2018-6-12
tags:
- Log
categories:
- Other
---

## 2018-6-12
1. 创建一个project和三个momodules
    * app android基础页面
    * test-robot robotium测试程序
    * test-uiautomator UiAutomator2测试程序

    adb shell
    pm list instrumentation

    adb shell am instrument -w com.ronnie.test_robot.test/android.test.InstrumentationTestRunner

    adb shell am instrument -w -r   -e debug false -e class 'com.ronnie.test_robot.RobotiumTest' com.ronnie.testdemo.test/android.test.InstrumentationTestRunner

2. Robotium无源码apk测试
```
task copyTask(type: Copy) {
    from 'app-debug.apk'//将被测试apk放在工程app目录下
    into 'build/outputs/apk/debug/'//将apk复制到指定目录
    rename { String fileName -> //在复制时重命名文件
        fileName = "app-debug.apk" // 重命名
    }
}
//修改  applicationId "com.ronnie.testdemo"为被测app的包名
//testInstrumentationRunner "android.test.InstrumentationTestRunner"
//运行-editconfiguration 在中间添加一个gradle:app:copyTask
```

### 参考资料
1. [Robotium在AndroidStudio中搭建及参数化测试实践](https://blog.csdn.net/xlyrh/article/details/52851037)
2. [Robotium (无源码)基于Android Studio 的自动化测试](https://github.com/ttraveler/robotium-as-demo/blob/master/tutorial/t2.md)
3. （https://github.com/ttraveler/robotium-as-demo）