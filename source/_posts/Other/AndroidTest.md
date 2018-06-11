---
title: Android Test
date: 2018-6-6
tags:
- 测试
- test
- Robotium
- Instrumentation
- UiAutomator
- UiAutomator2.0
categories:
- Other
---

### Instrumentation
* 通过Instrumentation你可以模拟按键按下、抬起、屏幕点击、滚动等事件。
* Instrumentation是通过将主程序和测试程序运行在同一个进程来实现这些功能，你可以把Instrumentation看成一个类似Activity或者Service并且不带界面的组件，在程序运行期间监控你的主程序。
* 缺点是对测试人员来说编写代码能力要求较高，需要对Android相关知识有一定了解，还需要配置AndroidManifest.xml文件，不能跨多个App。
### UiAutomator
Google提供的自动化测试框架，支持Android上的所有事件操作。可以跨App测试不能对Hybird App和WebApp测试
### Espresso
Espresso基于Instrumentation开发的
### Robotium
Robotium基于Instrumentation开发的不能跨app测试可以测试webapp

adb shell pm list instrumentation

## 步骤
1. 构造TestCast测试用例
2. 已经连接上AccessibilityService的UiDevice准备好
3. AccessibilityService监听事件并返回info信息。
4. UiAutomatorBridge通过UiAutomation提供的方法来获取AccessibilityNodeInfo信息
5. 通过translateCompoundSelector方法根据用户提供的UiSelector来遍历节点获取目标控件
6. 事件触发的时候才会去取节点信息，事件把控件节点的信息转换成控件的坐标点进行点击的


### 测试知识点记录
1. [AccessibilityService](https://www.jianshu.com/p/4cd8c109cdfb)
2. [Google AccessibilityService](https://developer.android.com/reference/android/accessibilityservice/AccessibilityService)


## 相关资料
1. [Android4.3引入的UiAutomation新框架官方简介](https://blog.csdn.net/zhubaitian/article/details/40504827)

2. [Robotium源码分析之Instrumentation进阶](https://blog.csdn.net/wanglha/article/details/42523855)
