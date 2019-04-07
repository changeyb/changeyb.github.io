---
layout: post
title:  "爬虫任务一"
categories: crawl
tags: crawl 爬虫
author: Benjamin
---

* content
{:toc}

加入DataWhale爬虫学习群，通过做任务的方式初步了解爬虫技术。




## 1.1 学习get与post请求
利用requests向https://www.baidu.com发送get请求。
```python
import requests
response = requests.get('https://www.baidu.com')
text, status_code = response.text, response.status_code
```
返回的结果`text`是`<!DOCTYPE html>\r\n<!--STATUS OK--><html> <head><meta http-equiv=content-type content=text/html;charset=utf-8><meta http-equiv=X-UA-Compatible content=IE=Edge><meta content=always name=referrer><link rel=stylesheet type=text/css href=https://ss1.bdstatic.com/5eN1bjq8AAUYm2zgoY3K/r/www/cache/bdorz/baidu.min.css><title>ç\x99¾åº¦ä¸\x80ä¸\x8bï¼\x8cä½\xa0å°±ç\x9f¥é\x81\x93</title></head> <body link=#0000cc> <div id=wrapper> <div id=head> <div class=head_wrapper> <div class=s_form> <div class=s_form_wrapper> <div id=lg> <img hidefocus=true src=//www.baidu.com/img/bd_logo1.png width=270 height=129> </div> <form id=form name=f action=//www.baidu.com/s class=fm> <input type=hidden name=bdorz_come value=1> <input type=hidden name=ie value=utf-8> <input type=hidden name=f value=8> <input type=hidden name=rsv_bp value=1> <input type=hidden name=rsv_idx value=1> <input type=hidden name=tn value=baidu><span class="bg s_ipt_wr"><input id=kw name=wd class=s_ipt value maxlength=255 autocomplete=off autofocus=autofocus></span><span class="bg s_btn_wr"><input type=submit id=su value=ç\x99¾åº¦ä¸\x80ä¸\x8b class="bg s_btn" autofocus></span> </form> </div> </div> <div id=u1> <a href=http://news.baidu.com name=tj_trnews class=mnav>æ\x96°é\x97»</a> <a href=https://www.hao123.com name=tj_trhao123 class=mnav>hao123</a> <a href=http://map.baidu.com name=tj_trmap class=mnav>å\x9c°å\x9b¾</a> <a href=http://v.baidu.com name=tj_trvideo class=mnav>è§\x86é¢\x91</a> <a href=http://tieba.baidu.com name=tj_trtieba class=mnav>è´´å\x90§</a> <noscript> <a href=http://www.baidu.com/bdorz/login.gif?login&amp;tpl=mn&amp;u=http%3A%2F%2Fwww.baidu.com%2f%3fbdorz_come%3d1 name=tj_login class=lb>ç\x99»å½\x95</a> </noscript> <script>document.write(\'<a href="http://www.baidu.com/bdorz/login.gif?login&tpl=mn&u=\'+ encodeURIComponent(window.location.href+ (window.location.search === "" ? "?" : "&")+ "bdorz_come=1")+ \'" name="tj_login" class="lb">ç\x99»å½\x95</a>\');\r\n                </script> <a href=//www.baidu.com/more/ name=tj_briicon class=bri style="display: block;">æ\x9b´å¤\x9aäº§å\x93\x81</a> </div> </div> </div> <div id=ftCon> <div id=ftConw> <p id=lh> <a href=http://home.baidu.com>å\x85³äº\x8eç\x99¾åº¦</a> <a href=http://ir.baidu.com>About Baidu</a> </p> <p id=cp>&copy;2017&nbsp;Baidu&nbsp;<a href=http://www.baidu.com/duty/>ä½¿ç\x94¨ç\x99¾åº¦å\x89\x8då¿\x85è¯»</a>&nbsp; <a href=http://jianyi.baidu.com/ class=cp-feedback>æ\x84\x8fè§\x81å\x8f\x8dé¦\x88</a>&nbsp;äº¬ICPè¯\x81030173å\x8f·&nbsp; <img src=//www.baidu.com/img/gs.gif> </p> </div> </div> </div> </body> </html>\r\n`

状态码`status_code`为``200``

断开网络再次请求后会出现一大串报错信息，主要的报错信息如下：

```python
ConnectionError: HTTPSConnectionPool(host='www.baidu.com', port=443): Max retries exceeded with url: / (Caused by NewConnectionError('<urllib3.connection.VerifiedHTTPSConnection object at 0x107597278>: Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known'))
```
简单来说就是由于网络连接的问题引发了错误。

### 1.1.1 状态码
HTTP状态码是用来表示网页服务器响应状态的3位数字代码。所有状态码的第一个数字代表了响应的五种状态之一。

#### 状态码的5种状态

| 状态码     | 说明     | 通俗解释 |
| :------------- | :------------- |:------------- |
| 1xx  | 响应中——表示请求已经接受，继续处理 |消息：一般是告诉客户端请求已经收到了，正在处理，别急|
| 2xx| 成功——表示请求已经被成功接收、理解、接受。 |处理成功：一般表示请求收悉、我明白你要的、请求已受理、已经处理完成等信息|
| 3xx | 重定向——要完成请求必须进行更进一步的操作|重定向到其它地方：它让客户端再发起一个请求以完成整个处理。|
| 4xx| 客户端错误——请求有语法错误或请求无法实现       |处理发生错误，责任在客户端：如客户端的请求一个不存在的资源，客户端未被授权，禁止访问等。|
| 5xx| 服务器端错误——服务器未能实现合法的请求。|处理发生错误，责任在服务端：如服务端抛出异常，路由出错，HTTP版本不支持等|



### 1.1.2 请求头
