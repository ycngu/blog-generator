---
title: 关于Cookie和Session以及响应头
date: 2018-12-26 15:36:54
tags: [javascript]
---
# Cookie 和 Session 的区别
Cookie是服务器通过Set-Cookie响应头给浏览器的一串字符串
浏览器访问相同域名时必须带上这段字符串
浏览器在一段时间内要保存Cookie
Cookie的大小大概在4KB左右
————————————————————
Session是服务器保存的
服务器通过Cookie给浏览器一个SessionID
服务器有一块内存保存了类似于 { SessionID：Session }的哈希数据结构
浏览器访问服务器时，服务器读取SessionID，根据ID找到对应的Session，服务器就可以读取Session中的用户信息了
# Cookie 和 LocalStorage 的区别？
Cookie是服务器通过Set-Cookie响应头给浏览器的一串字符串
浏览器访问相同域名时必须带上这段字符串
浏览器在一段时间内要保存Cookie
Cookie的大小大概在4KB左右
——————————————————————————————————————
LocalStorage是在浏览器本地保存的（可能保存在C盘之类的地方）并且和HTTP无关
只有在相同域名的页面才能互相读取LocalStorage，但是没有同源策略那么严格
LocalStorage如果用户不特意清除会永远保存
LocalStorage的大小大概在5MB左右
# LocalStorage 和 SessionStorage 的区别
LocalStorage是在浏览器本地保存的（可能保存在C盘之类的地方）并且和HTTP无关
只有在相同域名的页面才能互相读取LocalStorage，但是没有同源策略那么严格
LocalStorage如果用户不特意清除会永远保存
LocalStorage的大小大概在5MB左右
————————————————————————————————————————
SessionStorage和LocalStorage差不多，但是SessionStorage关闭页面就会消失
# Cookie 如何设置过期时间？
两种方法，设置Cache-Control或者设置Expires,设置Expires是老方法，现在推荐使用Cache-Control

Cache-Contro:
```javascript
response.setHeader('Cache-Contro','max-age=30')
```
Expires：
```javascript
response.setHeader('Expires','Wed, 26 Dec 2018 06:59:19 GMT')
```
两者的区别是前者规定过了多少时间后失效，后者是到了某个时间之后失效(后者指的是本地时间)
# 如何删除 Cookie？
可以用js来删除，也可以用户通过浏览器的清除缓存选项，把清除Cookie勾选上来删除。
还有Cookie过期了就自动删除了
# Cache-Control: max-age=1000 缓存 与 ETag 的「缓存」有什么区别？
Cache-Control: max-age=1000
在一千秒后Cookie会过期，在此期间除了第一次访问外，浏览器会直接从内存获取文件而不是通过Http请求，这个过程产生0流量
在一千秒后还得通过Http请求获取文件
——————————————————————————————
ETag相当于一个版本号，浏览器持有的这个版本号和服务器端一样的话就不用再重新下载文件了，但是和服务器端对比版本号这个过程会产生流量。
