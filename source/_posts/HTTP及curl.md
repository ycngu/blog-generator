---
title: HTTP及curl
date: 2018-09-29 23:21:42
tags: [javascript]
---
## 前言

![http.png](/images/HTTP及curl/1.png)

客户端   通过  请求  向服务器发送数据

服务器   通过  响应  向客户端返回数据
<!--more-->
## HTTP请求
HTTP请求包括四个部分

以下行 有1的是属于1的部分，有2的是属于2的部分以此类推

1 动词 路径 协议/版本  (实际上是这样的 GET / HTTP/1.1)
2 Key1: value1
2 Key2: value2
2 Key3: value3
2 Content-Type: application/x-www-form-urlencoded
2 Host: www.baidu.com
2 User-Agent: curl/7.54.0
3 
4 <!DOCTYPE html>
4<!--STATUS OK--><html> <head> 后面省略

1) 请求行：是一个ASCII文本行，由三个标记组成--请求的HTTP方法、URL、HTTP版本，之间用空格分开{GET /lovobook/index.html HTTP/1.0}；
2) 请求头：HTTP协议使用HTTP头来传递请求的元信息。HTTP头是一个用冒号分隔的名称/值对，冒号前面是HTTP头发名称，后面是HTTP的值；
3) 空行： 发送回车符和退行，通知服务器一下不再有请求头；
4) 消息体：  HTTP请求中带有查询字符串时，如果是GET方法，查询字符或表单数据附加值请求行中，则消息体中就没有内容；如果是POST方法，查询字符串或表单数据及添加在消息体中

![image.png](//video.jirengu.com/xdml/image/2a58d0d9-bca5-4d5d-9fbb-228e52484371/2018-9-29-20-15-53.png)

## HTTP响应
HTTP响应包括四个部分

1 协议/版本 状态码 原因短语 （实际上是这样的 HTTP/1.1 200 OK）
2 Accept-Ranges: bytes
2 Cache-Control: private, no-cache, no-store, proxy-revalidate, no-transform
2 Connection: Keep-Alive
2 Content-Length: 2443
2 Content-Type: text/html
2 Date: Tue, 10 Oct 2017 09:14:05 GMT
2 Etag: "5886041d-98b"
2 Last-Modified: Mon, 23 Jan 2017 13:24:45 GMT
2 Pragma: no-cache
2 Server: bfe/1.0.8.18
2 Set-Cookie: BDORZ=27315; max-age=86400; domain=.baidu.com; path=/
3
4<!DOCTYPE html>
4<!--STATUS OK--><html> <head> 后面省略

1) 状态行：以一个状态行开头。状态行有HTTP协议版本、响应状态码和响应描述组成，之间用空格分隔；
2) 响应头：与请求头一样；
3) 空白行：最后一个响应头之后是一个空行，发送回车符和退行，表明以下不再有响应头；
4) 消息体：要发送回BS的HTTP文档或其它要显示的内容等。Web服务器把要发送给客户端的文档信息放在消息体中。

![image.png](//video.jirengu.com/xdml/image/2a58d0d9-bca5-4d5d-9fbb-228e52484371/2018-9-29-20-20-51.png)

## 如果想详细了解HTTP状态码和各字段的意义
请去看 《图解HTTP》！！！

## 用Chrome开发者工具查看 HTTP 响应/请求 内容

按键盘上的F12，会弹出开发者工具，输入网址，如 www.baidu.com 回车
点击network，点击www.baidu.com，找到Request Headers，会看到如下场景

![baidu1.png](//video.jirengu.com/xdml/image/2a58d0d9-bca5-4d5d-9fbb-228e52484371/2018-9-29-21-14-30.png)

再点击view source，你就会看到请求内容了

![baidu2.png](//video.jirengu.com/xdml/image/2a58d0d9-bca5-4d5d-9fbb-228e52484371/2018-9-29-20-55-43.png)

查看响应内容同理，找到Request Headers ，点击view source


![baidu3.png](//video.jirengu.com/xdml/image/2a58d0d9-bca5-4d5d-9fbb-228e52484371/2018-9-29-21-20-28.png)

## 使用curl
curl是一种从服务器传输数据或向服务器传输数据的命令行工具
用它可以像浏览器那样向服务器发起请求
下面是curl命令的常用选项

-A/--user-agent <string> 设置用户代理发送给服务器，即告诉服务器浏览器为什么
    -basic 使用HTTP基本验证
    --tcp-nodelay 使用TCP_NODELAY选项
    -e/--referer <URL> 来源网址，跳转过来的网址
    --cacert <file> 指定CA证书 (SSL)
    --compressed 要求返回是压缩的形势，如果文件本身为一个压缩文件，则可以下载至本地
    -H/--header <line>自定义头信息传递给服务器
    -I/--head 只显示响应报文首部信息
    --limit-rate <rate> 设置传输速度
    -u/--user <user[:password]>设置服务器的用户和密码
    -0/--http1.0 使用HTTP 1.0
    -s --silent 静默模式,不显示错误和进度
    -x 指定请求方式，如GET POST PUT等等
    
    例子
    curl -s   -- "https://www.baidu.com"

输入上面的命令后，curl会向百度的服务器发起GET请求（默认是GET）
返回的报文主体如下
![curl1.png](//video.jirengu.com/xdml/image/2a58d0d9-bca5-4d5d-9fbb-228e52484371/2018-9-29-21-47-47.png)










