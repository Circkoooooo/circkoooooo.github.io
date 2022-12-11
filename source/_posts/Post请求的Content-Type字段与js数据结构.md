---
layout: http
title: Post请求的Content-Type字段与js数据结构
date: 2022-12-11 20:50:10
tags:
	- javascript
	- 基础
---

在使用fetch或者XMLHttpRequest，或者封装好的一些Http请求的工具的时候，如果我们发送POST请求，通常会携带一些数据在请求头的Body中，这时我们需要在Content-Type字段中去指定对应的编码标头来让接收端区分用哪种方式去解析。

大多数情况下我们会发送的有（默认格式）表单数据编码格式，json等等。

## 默认表单数据格式（x-www-form-urlencoded）
如果传输数据是form表单格式，则Content-Type可以省略。
发送格式则是如`param=value&param2=value2`的形式。
### 怎么传输该格式的数据？
1. html中post表单提交
html中使用post表单，提交表单后请求中将会携带该数据格式的body。**但是如果我们需要使用ajax，那我们可能会在js中处理请求，也会在js中来组合数据，所以可能需要使用另外的方式，也就是下面的UrlSearchParams**。
2. FormData
在js中封装了FormData这样一个类，`const data = new FormData()`创建，可以通过`data.append(name,value,[filename])`来设置值,其中value可以是form表单中对应的格式，而不是限制于string类型。
3. UrlSearchParams
它和formdata比较类似，不过它通常用于get请求，因为它传输的数据为query形式，也就是`param=value&parama2=value2`...
`const params = new UrlSearchParams`创建，通常使用`params.append()`来添加key-value值，`params.get()`来获取key-value值，更详细可以去mdn查看。

## JSON格式（application/json）
`json是用于前后端分离的很常见的一个数据格式，所以在前后端可以很方便的通过json的规则去解析或者合成json。`

1. Content-Type对应值
`application/json;chatset=UTF-8`

2.  在js中使用JSON类中提供的`stringify`和`parse`函数就能将一个对象转成json格式（这里不考虑循环引用之类的问题），或者将json转化成一个对象形式。