---
title: CSS布局之水平居中
date: 2018-11-16 07:39:49
tags:
---
CSS中居中方式多种多样，我们需要根据情况选择合适的方式与技巧，本文介绍了一些常用的居中方式。
# 水平居中
## inline或者inline-block元素
这种就比较简单了，直接使用`text-align: center;`即可。 
![](http://ww1.sinaimg.cn/large/abbc1cebgy1fx9jlobra9j20mq054dft.jpg)
![](http://ww1.sinaimg.cn/large/abbc1cebgy1fx9jmx9uh3j20be03k0sm.jpg)
## 一个block元素
给`margin-left`和`margin-right`一个`auto`值（**但这个块必须得有`width`**）
![](http://ww1.sinaimg.cn/large/abbc1cebgy1fx9jpth2vyj20mt055glk.jpg)
![](http://ww1.sinaimg.cn/large/abbc1cebgy1fx9jrd1r86j20mo05k0sr.jpg)
要注意的是`float`属性<b>没有center这个值</b>，所以你不能把一个元素浮动到center
## 多个block元素
可以使用`inline-block`或者flex布局： <br>
1. `inline-block` <br>
给父元素`text-align: center;`给子元素`display： inline-block`

1. flexbox布局 <br>
父元素这样设置：
```CSS
.flex-center{
  display: flex;
  justify-content: center;
}
```
子元素得设置`max-width`
<br><br>
以上两种方法居中对比：![](http://ww1.sinaimg.cn/large/abbc1cebgy1fx9kfu1rrmj20co0fnt9e.jpg)










