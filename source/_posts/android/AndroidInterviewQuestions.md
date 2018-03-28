---
title: Android 题库
date: 2018-01-13
tags:
- 算法
- Android
categories:
- Android
---

#### 算法
[leetcode](https://github.com/dark74/Awesome-java-leetcode)
#### [Activity启动流程全解析](http://blog.csdn.net/luoshengyang/article/details/6689748)
#### String Stringbuffer Stringbuilder区别
* String 字符串常量，字符串长度不可变
* StringBuffer 线程安全的可变字符序列，常用的方法toString(),append(),insert()
* StringBuilder 非线程安全字符串
* String是不可变对象，因此每次对String类型进行改变的时候，都会生成一个新的String对象，然后将指向新的String对象，所以经常改变内容的字符串最好不要使用String使用String。
* 使用原则操作少的使用String，单线程操作大量数据使用StringBuilder，多线程使用StringBuffer

#### Activity的启动模式
* standard 默认启动方式，每次启动activity都会启动一个新的实例，并放在栈结构的顶部。
* singleTop 当启动一个activity的时候如果栈中存在并在栈顶，则重复利用，如果存在但不在栈顶就创建一个新的实例
* singleTask 当启动一个activity的时候系统发现存在这个实例则不会创建新的实例，而是将骑上的activity统统出栈，如果找不到则创建新实例。
* singleInstance 启动一个activity为其创建一个新栈。

#### 如何配置Activity的启动模式
* 在AndroidManifest.xml配置android:launchMode属性
*  在startActivity的intent中添加flag
```
    Intent qIntent =new Intent(this, QMUIActivity.class);
    qIntent.setFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP)
    tartActivity(qIntent);
```

#### Android服务两种启动方式的区别
##### startService的方式
##### 使用Service的步骤
```
     1. 定义一个类继承Service
     2. 在Manifest.xml文件中配置该Service
     3. 使用Context的startService(Intent)方法启动该Service
     4. 调用stopService(Intent)方法停止该服务
 ```
##### 使用start方式的声明周期 onCreate() ->onStartCommand -> onDestory() 如果服务已经启动不会重复执行onceate()方法而是会调用onStart()和onStartCommand();
##### 特点一旦服务启动就和开启者没有关系了，开启者退出也不会影响到服务服务还在后台运行。

##### bindService的方式
##### 使用Service的步骤
```
    1. 定义一个类继承Service
    2. 在Manifest.xml文件中配置该Service
    3. 使用Context的bindService(Intent, ServiceConnection, int)方法启动该Service
    4. 不再使用时，调用unbindService(ServiceConnection)方法停止该服务
```
##### 使用这种bind方式启动的Service的生命周期 onCreate() ->onBind()->onunbind()->onDestory()
##### 特点bind的方式开启服务，绑定服务，调用者挂了，服务也会跟着挂掉。绑定者可以调用服务里面的方法。

#### Android两种注册、发送广播的区别
##### 代码中动态注册
1. 实例化自定义的广播接受者
2. 实例化意图过滤器，并设置要过滤的广播类型
3. 使用Context的registerReceiver(BroadcastReceiver,IntentFilter,String,Handler)方法注册广播
###### 广播跟随程序的生命周期
##### 在Manifest.xml中静态注册
```
    <receiver android:name=".MyBroadCastReceiver">
        <intent-filter android:priority="20">
        <actionandroid:name="android.provider.Telephony.SMS_RECEIVED"/>
        </intent-filter>
    </receiver>
```
###### 常驻型广播，程序关闭后，如果有信息广播来，程序也会被系统调用自动运行。
##### 发送广播
###### 无序广播 Context.sendBroadcast(Intent)或Context.sendBroadcast(Intent,String)发送的无需广播添加了权限，无序广播所有的接受者都会接收事件，不可以被拦截，不可以被修改。
###### 有序广播 Context.sendOrderedBroadcast(Intent,String,BroadCastReceiver,Handler,int,String,Bundle)给每个接收者设置优先级，就可以在小于自己优先级的接收者得到广播前修改或终止广播。

#### http和https的区别
1. HTTP 的 URL 以 http:// 开头，而 HTTPS 的 URL 以 https:// 开头
2. HTTP 是不安全的，而 HTTPS 是安全的
3. HTTP 标准端口是 80 ，而 HTTPS 的标准端口是 443
4. 在 OSI 网络模型中，HTTP 工作于应用层，而 HTTPS 工作在传输层
5. HTTP 无需加密，而 HTTPS 对传输的数据进行加密
6. HTTP 无需证书，而 HTTPS 需要认证证书

#### Android进程保活
1. 不同app进程，用广播相互唤醒
2. 启动前台service（在系统的通知栏产生一个Notification，用来让用户知道app在运行）
3. 利用系统的漏洞启动前台service（不会产生一个Notification，看起来就如同一个后台的service）
```
思路一：API < 18，启动前台Service时直接传入new Notification()；
思路二：API >= 18，同时启动两个id相同的前台Service，然后再将后启动的Service做stop处理；
```

#### 进程通信的方式
1. [AIDL](http://blog.csdn.net/lmj623565791/article/details/38461079)
2. [广播](http://blog.csdn.net/lmj623565791/article/details/47017485)
3. Messenger

#### 三级缓存
1. 内存
2. 本地
3. 网络

#### 浅谈MVC MVP MVVM

#### java虚拟机和Dalvik
* java虚拟机运行的是java字节码，Dalvid虚拟机运行的是Dalvid字节码。传统的java程序经经过编译，生成java字节码保存在class中。java虚拟机通过解码class文件中的内容来运行。而Dalvik虚拟机运行的是Dalvik码，所有的Dalvik字节码由java字节码转换过来的，并被打包到一个DEX可执行文件中，Dalvik虚拟机通过解析DEX文件来这行这些字节码。
* Dalvik可执行文件体积更小。SDK中有一个dx的工具负责将java字节码转换为Dalvik字节码
* java虚拟机与Dalvik虚拟机架构不同。java虚拟机基于栈结构。程序在运行时虚拟机需要频繁的从栈顶上读取或写入数据。这个过程需要更多的指令分配与内存访问次数，会耗费不少CPU时间。Dalvik虚拟机基于寄存器架构，数据的访问通过寄存器直接传递，这样的访问方式比基于栈的方式快的多。

#### sleep和wait有什么区别
1. 都是用来进行线程控制，他们最大的区别是sleep不释放同步锁，wait释放同步锁。
2. sleep(milliseconds)可以用时间指定他自动醒过来，如果时间不到只能调用interreput来强行打断，wait可以使用notify直接唤醒。
3. sleep是Thread类的静态方法，wait是object的方法。

#### View,ViewGroup事件分发

#### 保持Activity状态
onSaveInstanceState()

#### 内存泄漏检测，内存性能优化
1. 节制的使用Service（IntentService：特点是当后台任务结束后自动停止）
2. 在Activity中重写onTrimMemory方法监听TRIM_MEMORY_UI_HIDDEN这个级别，触发了之后说明用户离开了我们的程序，那么就可以世行资源。
3. 尽量避免渲染高分辨率的图片。
4. 使用优化过的数据结合如：SparseArray,SparseBooleanArray以及LongSpareArray
5. 了解内存的使用情况
     * 枚举比使用静态常量要消耗两倍以上的内存
     * 任何一个类包括内部类匿名类都要暂用大约500字节的内存
     * 任何一个类的实例都要消耗12-16字节的内存
     * 在用HashMap时即使你设置一个基本数据类型作为键他也会按照对象大小来分配内存32字节。
6. 谨慎使用抽象编程
7. 尽量避免使用依赖注入框架
8. 使用ProGuard简化代码，它除了混淆代码还可以压缩和优化代码。


#### 布局优化
1. <include> 如果需要在标签中覆写laout属性，必须将layout_width和layout_height两个属性进行覆写，否则覆写不会生效
2. <merge>  标签作为include标签的一种辅助扩展使用，它主要是防止在引用布局文件时产生多余的布局嵌套。
3. <ViewStub>仅在需要的时候加载布局，所加载的布局不能使用<merge>标签的

#### String，StringBuffer，StringBuilder
1. String不可变对象，每次赋值连接字符串都会产生新的字符串
2. StringBuffer线程安全
3. StringBuilder线程不安全 效率高 推荐单线程时使用

#### java设计模式