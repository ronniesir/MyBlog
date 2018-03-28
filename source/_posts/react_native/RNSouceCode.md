---
title: React Native 从源代码开始编译
date: 2017-12-13
tags:
- 移动开发
- React Native
categories:
- React Native
---
### 基础环境
#### 1、Android SDK版本Version 23 (build.gradle文件中compileSdkVersion标签版本号)
#### 2、SDK build tools Version 23.0.1 (build.gradle文件中buildToolsVersion标签版本号)
#### 3、Android Support Repository>=17(Android支持库)
#### 4、Android NDK（NDK-r10e版本）
### 配置
#### 1、android项目根目录上build.gradle添加gradle-download-task依赖下载插件
```
    dependencies {
        classpath 'com.android.tools.build:gradle:1.3.1'
        classpath 'de.undercouch:gradle-download-task:2.0.0'
    }
```
#### 2、android项目setting.gradle中添加如下依赖
```
include ':ReactAndroid'
project(':ReactAndroid').projectDir = new File(
    rootProject.projectDir, '../node_modules/react-native/ReactAndroid')
```
#### 3、修改所有库下面的react-native依赖，把 compile 'com.facebook.react:react-native:0.16.+'改为comple project(':ReactAndroid')
```
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.android.support:appcompat-v7:23.0.1'
    compile project(':ReactAndroid')
}
```
#### 4、修改android项目和ReactAndroid项目下的local.properties文件中的ndk路径为本机绝对路径
```
例如：ndk.dir=/Users/ronnie/android-ndk-r10e
```
#### 5、复制node_modules/react-native/ReactCommon到ReactAndroid项目下，并修改ReactAndroid中build.gradle中的配置，将$projectDir/../ReactCommon修改为$projectDir/ReactCommon
```
task buildReactNdkLib(dependsOn: [prepareJSC, prepareBoost, prepareDoubleConversion, prepareFolly, prepareGlog], type: Exec) {
       inputs.file('src/main/jni/react')
       outputs.dir("$buildDir/react-ndk/all")
       commandLine getNdkBuildFullPath(),
               'NDK_PROJECT_PATH=null',
               "NDK_APPLICATION_MK=$projectDir/src/main/jni/Application.mk",
               'NDK_OUT=' + temporaryDir,
               "NDK_LIBS_OUT=$buildDir/react-ndk/all",
               "THIRD_PARTY_NDK_DIR=$buildDir/third-party-ndk",
               "REACT_COMMON_DIR=$projectDir/ReactCommon",
               '-C', file('src/main/jni/react/jni').absolutePath,
               '--jobs', project.hasProperty("jobs") ? project.property("jobs") : Runtime.runtime.availableProcessors()
   }

```
### 参考
#### [React Native基础之从源代码编译详解](http://www.lcode.org/react-native%E5%9F%BA%E7%A1%80%E4%B9%8B%E4%BB%8E%E6%BA%90%E4%BB%A3%E7%A0%81%E7%BC%96%E8%AF%91%E8%AF%A6%E8%A7%A3-%E9%80%82%E9%85%8Dandroid%E5%BC%80/)
#### [React Native For Android 源码编译](https://www.jianshu.com/p/bd4bcdceba9b)