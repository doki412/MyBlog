---
title: HTTP请求与响应
date: 2018-08-07 12:08:48
tags:
---
# Server+Client+HTTP简述
![](http://ww1.sinaimg.cn/large/abbc1cebly1fu0w0r54jwj21590ixdn3.jpg)

* 浏览器负责发起请求
* 服务器在 80 端口接收请求
* 服务器负责返回内容（响应）
* 浏览器负责下载响应内容
<br>**HTTP 的作用就是指导浏览器和服务器如何进行沟通。**

# curl的使用
## 作用
explainshell.com中对`curl`的解释:
![](http://ww1.sinaimg.cn/large/abbc1cebly1fu0wxucxstj21880hlta6.jpg)
## 选项
```
-s --silent
       Silent or quiet mode. Don't show progress meter or error messages.  Makes Curl mute.
（不显示进度条）

transfer a URL
-s, --silent
       Silent or quiet mode. Don't show progress meter or error messages.  Makes Curl mute.
-v, --verbose
       Makes  the  fetching more verbose/talkative. Mostly useful for debugging. A line starting with '>'  means "header data" sent by curl, '<' means "header data" received  by  curl  that  is  hidden
 in normal cases, and a line starting with '*' means additional info provided by curl.
（显示请求和响应，没有则只显示响应）
-H --header <header>
       (HTTP) Extra header to use when getting a web page. You may specify any number of  extra  headers.Note  that  if  you  should add a custom header that has the same name as one of the internal ones curl would use, your externally set header will be used instead of the internal one.  This  allows you to make even trickier stuff than curl would normally do. You should not replace internally set headers without knowing perfectly well what you're doing. Remove an internal header  by  giving a replacement without content on the right side of the colon, as in: -H "Host:".

       curl  will  make sure that each header you add/replace is sent with the proper end-of-line marker,you should thus not add that as a part of the header content: do  not  add  newlines  or  carriage returns, they will only mess things up for you.

       See also the -A, --user-agent and -e, --referer options.

       This option can be used multiple times to add/replace/remove multiple headers.
（响应头）
```


# 请求
## curl命令查看请求
### get请求
```
$ curl -s -v -H "ju:111" -- "https://www.baidu.com"
```
运行该命令行例句得到的请求部分：
![](http://ww1.sinaimg.cn/large/abbc1cebly1fu0xjico09j20o403ijrq.jpg)


请求格式为：<br>
```
1 动词 路径 协议/版本<br>
2 Key1: value1<br>
2 Key2: value2<br>
2 Key3: value3<br>
2 Content-Type: application/x-www-form-urlencoded
2 Host: www.baidu.com
2 User-Agent: curl/7.54.0
3 <br>
4 要上传的数据
```
1. 请求最多包含四部分，最少包含三部分。（也就是说第四部分可以为空）
2. 第三部分永远都是一个回车（\n）
3. 动词有 GET POST PUT PATCH DELETE HEAD OPTIONS 等
4. 这里的路径包括「查询参数」，但不包括「锚点」
5. 如果你没有写路径，那么路径默认为 /
6. 第 2 部分中的 Content-Type 标注了第 4 部分的格式
### POST请求
```
$ curl -X POST -s -v -H "ju:111" -- "https://www.baidu.com/s?wd=javascript#6"

```
运行后得到的请求部分：<br>
![](http://ww1.sinaimg.cn/large/abbc1cebly1fu0yccy4ykj20jb03j3yr.jpg)<br>
是的，你发现了，路径中**包含查询参数但是不包含锚点**


## Chrome浏览器查看请求
方法：
1. 打开 Network
1. 地址栏输入网址
1. 在 Network 点击，查看 request，点击「view source」
1. 如果有请求的第四部分，那么在 FormData 或 Payload 里面可以看到


你会看到这样的结果：<br>
![](http://ww1.sinaimg.cn/large/abbc1cebly1fu0yiguhhsj21cg0a0wfr.jpg)


# 响应
## curl命令查看响应
响应的格式：<br>
```
1 协议/版本号 状态码 状态解释
2 Key1: value1
2 Key2: value2
2 Content-Length: 17931
2 Content-Type: text/html
3
4 要下载的内容
```
* 状态码要背，是服务器对浏览器说的话
    * 1xx 不常用。
    * 2xx 表示成功。 其中 200、204表示创建成功
    * 3xx 表示滚吧。 其中 301表示搬走了，302表示临时不存在，304表示这一次响应内容和上一次的一样
    * 4xx 表示你丫错了。  如404  
    * 5xx 表示好吧，我错了。 如502
* 状态解释没什么用
* 第 2 部分中的 Content-Type 标注了第 4 部分的格式
* 第 2 部分中的 Content-Type 遵循 MIME 规范


例如之前两个`curl`命令行得到的响应部分分别为：
![](http://ww1.sinaimg.cn/large/abbc1cebly1fu0za1nq14j20rb07x3zn.jpg)
（后面为网页源码）
![](http://ww1.sinaimg.cn/large/abbc1cebly1fu0zqm79e4j20ri06ojrx.jpg)
*  GET 请求和 POST 请求对应的响应可以一样，也可以不一样
* 响应的第四部分可以很长很长很长

## Chrome浏览器查看响应
方法：
1. 打开 Network
1. 输入网址
1. 选中第一个响应
1. 查看 Response Headers，点击「view source」，点击「view source」，点击「view source」
1. 你会看到响应的前两部分
1. 查看 Response 或者 Preview，你会看到响应的第 4 部分

你会看到这样的结果：
![](http://ww1.sinaimg.cn/large/abbc1cebly1fu1032dcarj21ce0bmq49.jpg)