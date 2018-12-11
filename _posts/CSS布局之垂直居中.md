---
title: CSS布局之垂直居中
date: 2018-11-16 08:04:34
tags:
---
# 垂直居中
## inline元素
### 单行
1. 上下padding设置为一样的。
1. 或者：
```CSS
centre-text-trick{
    height： 100px;
    line-height: 100px;
    white-space: nowrap;
}
```

### 多行
父元素设固定高
```CSS
.flex-center-vertically{
    display: flex;
    justify-content: center;
    flex-direction: column;
    height:400px;
}
```
## block元素
* 知道高度： 
```CSS
.parent{
    position: relative;
}
.child{
    position: absolute;
    top: 50%;
    height: 100px;
    margin-top: -50px;          /*height的一半*/
}
```
* 不知道高度：
```CSS
.parent{
    position: relative;
}
.children{
    position: absolute;
    top: 50%;
    transform: translate Y(-50%);
}
```
CSS中的轴：
![](http://ww1.sinaimg.cn/large/abbc1cebgy1fy2kyqijk6j20cd0bqjtv.jpg)

* flex布局：
```CSS
.parent{
    display: flex;
    justify content: center;
    align-items: center;
}
```