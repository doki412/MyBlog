---
title: HTML的一些常用标签
date: 2018-09-08 00:05:00
tags:
---
# a标签
用法例子：`<a href=""https://qq.com target="_blank">QQ</a>`
## target属性
对于a标签的`target`属性主要有4种`value`:<br>
1. `_blank 表示在新页面打开`
1. `_self 表示在当前页面打开`
1. `_parant 表示在父页面打开`
1. `_top 表示在顶层页面打开`
## download属性
1. 该属性可以不赋值使用，例如`<a href='index_logo.gif' download>下载logo</a>`。
1. 也可以赋值使用，比如`<a href='index_logo.gif' download="111.gif">下载logo</a>`来指定下载图片的文件名，如果后缀名一样则还可以省略后缀变为`download="111"`。
## href属性
该属性为a标签必须声明的属性，主要有以下几种用法：
```html
1.  href="//qq.com"    无协议的绝对地址（将继承当前协议）
2.  href="xxx.html"    这是一个相对地址，将跳转到当前目录下的xxx.html
3.  href="#1111"    当前文件后加锚点（该跳转不发起请求）
4.  href="?name=doki"   加了查询参数，这是正确的写法并且发起了一个GET请求
5.  href=""    跳转到自身（刷新页面）
6.  href="javascript:alert(1);"     在href中写伪协议，'javascript:'后面直接写代码，注意代码以';'结尾，这种情形下有一种用法：href="javascript:;"其结果是什么都不做
```
# form标签
与a标签不同的是，a标签发起的是一个GET请求，而form标签发起的是一个POST请求。
```html
<form action="index2.html" method="post">
    <input type="text" name="xxx">
    <input type="password" name="yyy">
    <input type="submit" value="提交">
</form>
```
这是运行的效果：
![](http://ww1.sinaimg.cn/large/abbc1cebly1fv6tap6wnjj21gb0l4wgz.jpg)<br>
注意：form表单中若无提交按钮则无法提交form
<br>
* 如果GET，会把输入的name直接当做查询参数
* 如果POST，会把输入的name放进请求的第四部分作为值<br>
form也可以有`target`，也可以放在`<iframe>`中
## 关于`<button>`按钮
`<button>`如果没有`type=button`则会自动升级为submit按钮，如果有`type="button"`则form表单会没有提交按钮且因而不会被提交。在`<input>`中`type="submit"`是唯一能够让表单提交的type。<br>
与`<input>`相比，`<button>`可以有`<span>`等子元素，而`<input>`没有子元素。
## `<select>`下拉列表
用法举例：
```html
<select name="group" multiple>      <!--mutiple意为可多选-->
    <option value="">-<option>
    <option value="1">第一组</option>
    <option value="2">第二组</option>
    <option value="3" disabled>第三组</option>      <!--disabled意为无法被选中-->
    <option value="4" selected>第四组</option>      <!--selected意为在页面加载时被预先选定-->
</select>
```
效果如图：![](http://ww1.sinaimg.cn/large/abbc1cebly1fv769636dpj20ci09hdfs.jpg)
# table标签
一个table的栗子：
```html
<table border=1>
    <colgroup>
        <col width=100>
        <col bgcolor=red width=200>
        <col width=100>
        <col width=70>
    </colgroup>
    <thead>
        <tr>
        <th>项目</th><th>姓名</th><th>班级</th><th>总分</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th></th><td>小明</td><td>1</td><td>94</td>
        </tr>
        <tr>
            <th></th><td>小红</td><td>2</td><td>96</td>
        </tr>
        <tr>
            <th>平均分</th><td></td><td></td><td>95</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <th>总分</th><td></td><td></td><td>190</td>
        </tr>
    </tfoot>
</table>
```
效果如图：
![](http://ww1.sinaimg.cn/large/abbc1cebly1fv76uu7wiij20na09jt92.jpg)