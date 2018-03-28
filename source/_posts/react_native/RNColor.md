---
title: React Native 基础
date: 2017-03-13
tags:
- 移动开发
- React Native
categories:
- React Native
---

### 颜色
以下这些格式的颜色代码都是支持的：
* '#f0f' (#rgb)
* '#f0fc' (#rgba)
* '#ff00ff' (#rrggbb)
* '#ff00ff00' (#rrggbbaa)
* 'rgb(255, 255, 255)'
* 'rgba(255, 255, 255, 1.0)'
* 'hsl(360, 100%, 100%)'
* 'hsla(360, 100%, 100%, 1.0)'
* 'transparent'
* 'red'
* 0xff00ff00 (0xrrggbbaa)
### 图片
#### 本地图片
``` 
<Image source={require('./my-icon.png')} style={{width: 40, height: 40}} />
```
#### 网络图片（必须手动指定图片的尺寸）
``` 
<Image source={{uri: 'app_icon'}} style={{width: 40, height: 40}} />
```
#### 图片命名
>  如果你有my-icon.ios.png和my-icon.android.png，Packager就会根据平台而选择不同的文件.
> 你还可以使用@2x，@3x这样的文件名后缀，来为不同的屏幕精度提供图片。
##### 注意：如果你添加图片的时候packager正在运行，可能需要重启packager以便能正确引入新添加的图片。
##### 这样会带来如下的一些好处:
* iOS和Android一致的文件系统。
* 图片和JS代码处在相同的文件夹，这样组件就可以包含自己所用的图片而不用单独去设置。
* 不需要全局命名。你不用再担心图片名字的冲突问题了。
* 只有实际被用到（即被require）的图片才会被打包到你的app。
* 现在在开发期间，增加和修改图片不需要重新编译了，只要和修改js代码一样刷新你的模拟器就可以了。
* 与访问网络图片相比，Packager可以得知图片大小了，不需要在代码里再声明一遍尺寸。
* 现在通过npm来分发组件或库可以包含图片了。
>  注意：为了使新的图片资源机制正常工作，require中的图片名字必须是一个静态字符串（不能使用变量！因为require是在编译时期执行，而非运行时期执行！）
#### 混合app图片资源的使用
##### 注意：这一做法并没有任何安全检查。你需要自己确保图片在应用中确实存在，而且还需要指定尺寸。
##### 1、Android的drawable目录下的资源和xcode的asset类目中的资源，引用方式：直接使用文件名，不带路径和后缀
``` 
<Image source={{uri: 'app_icon'}} style={{width: 40, height: 40}} />
```
##### 2、  Android的assets目录下的资源，引用方式还可以使用asset:/前缀来引用：
``` 
<Image source={{uri: 'asset:/app_icon.png'}} style={{width: 40, height: 40}} />
```
