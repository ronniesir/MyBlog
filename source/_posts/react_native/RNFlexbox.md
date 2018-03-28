---
title: React Native Flexbox
date: 2017-03-12
updated: 2017-12-20	
tags:
- 移动开发
- React Native
categories:
- React Native
---
###  基础概念
容器默认存在两根轴：主轴和交叉轴，和容器方向保持一致的叫做主轴，反之叫做交叉轴。
###  元素属性
* flexDirection 决定容器的主轴方向及容器的排列方向
    * row（默认值）：横向排列，主轴为水平方向，起点在左端。
    * row-reverse：横向排列，主轴为水平方向，起点在右端。
    * column：纵向排列，主轴为垂直方向，起点在上沿。
    * column-reverse：纵向排列，主轴为垂直方向，起点在下沿。
* flex-wrap（flexWrap）
    * wrap 元素满一行自动换行
    * nowrap 元素满一行不换行，超出部分隐藏
* flexGrow
    * 定义元素的放大比例，默认为0，如果存在剩余空间也不放大
    * 如果所有元素都设置为1等分剩余空间，权重越大分配的比例越高
* flexShrink
    * 定义元素的缩放比例，如果空间不够按比例缩放，如果设置为0不缩放
* flexBasis
* flex 值不能为负值

* justifyContent 决定了子元素在主轴的排列方式(假定主轴是横向的)
    * flex-start  左对齐
    * center 居中对齐
    * flex-end 右对齐
    * space-around 子元素左右两边等距
    * space-between 两端对齐
    
* alignItems 决定了子元素在交叉轴上的排列方式(假定交叉轴是纵向)
    * flex-start：居上对齐
    * center：居中排列
    * flex-end：居下对齐
    * stretch：拉伸。注意如果如果子元素使用此属性，就不能设置固定的尺寸
    
* borderBottomWidth 下方边框宽度
* borderLeftWidth 左侧方框宽度
* borderRightWidth 右侧方框宽度
* borderTopWidth 上方边框宽度
* borderWidth 边框宽度

* alignSelf决定了元素相对于父元素在交叉轴上的排列方式 (假定交叉轴是纵向的)
    * auto
    * flex-start 居上
    * flex-end 居下
    * center 居中
    * stretch 拉伸
* position：absolute，relative
* left 本组件定位到左边多少个像素（左边的定义取决于positon属性）
* bottom 本组件定位到下边多少个像素（下边的定义取决于positon属性）
* right 本组件定位到右边多少个像素（右边的定义取决于positon属性）
* top 本组件定位到上边多少个像素（上边的定义取决于positon属性）
* zIndex 
* height 元素的高度
* width 元素的宽度
* margin 组件与组件之间的距离
* marginBottom
* marginLeft
* marginRight
* marginTop
* marginVertical
* marginHorizontal
* maxHeight 最大高度
* maxWidth 最大宽度
* minHeight 最小高度
* minWidth 最小宽度
* padding 组件与内容的距离
* paddingBottom
* paddingHorizontal
* paddingLeft
* paddingRight
* paddingTop
* paddingVertical
* overflow 控制子元素的显示和大小
    * visible 改变大小，超出部分可见
    * hidden 超出部分隐藏
    * scroll 超出部分滑动


 

