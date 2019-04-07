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

### 1.1.1状态码
HTTP状态码是用来表示网页服务器响应状态的3位数字代码。所有状态码的第一个数字代表了响应的五种状态之一。

#### 状态码的5种状态

| 状态码     | 说明     | 通俗解释 |
| :------------- | :------------- |:------------- |
| 1xx  | 响应中——表示请求已经接受，继续处理 |消息：一般是告诉客户端请求已经收到了，正在处理，别急|
| 2xx| 成功——表示请求已经被成功接收、理解、接受。 |处理成功：一般表示请求收悉、我明白你要的、请求已受理、已经处理完成等信息|
| 3xx | 重定向——要完成请求必须进行更进一步的操作|重定向到其它地方：它让客户端再发起一个请求以完成整个处理。|
| 4xx| 客户端错误——请求有语法错误或请求无法实现       |处理发生错误，责任在客户端：如客户端的请求一个不存在的资源，客户端未被授权，禁止访问等。|
| 5xx| 服务器端错误——服务器未能实现合法的请求。|处理发生错误，责任在服务端：如服务端抛出异常，路由出错，HTTP版本不支持等|

#### 常见的状态码

| 状态码     | 说明     |
| :------------- | :------------- |
| 200       | 客户端请求成功，即处理成功       |
| 404       | 请求资源不存在，eg：输入了错误的URL，找不到页面或者页面已经被网站删除了      |

### 1.1.2 请求头
http请求头，HTTP客户程序（例如浏览器），向服务器发送请求的时候必须指明请求类型（一般是GET或者POST）。如有必要，客户程序还可以选择发送其他的请求头。

#### 常见的请求头


| 请求头 | 说明    |事例|状态|
| :------------- | :------------- | :------------- | :------------- |
| User-Agent      | 浏览器的身份标识字符串|User-Agent: Mozilla/……|固定|
|Accept|可接受的响应内容类型（Content-Types）|Accept:text/plain|固定|
|Accept-Charset|可接受的字符集|Accept-Charset:utf-8|固定|
|Accept-Encoding|可接受的响应内容的编码方式|Accept-Encoding:gzip,deflate|固定|
|Accept-Language|可接受的响应内容语言列表|Accept-Language:en-US|固定|
|Connection|客户端（浏览器）想要优先使用的连接类型|Connection: keep-alive|固定|

#### 添加请求头的方式
`requests`中添加请求头比较方便，只要简单地传递一个 dict 给 headers 参数就可以了。
事例如下：

```python
import requests
url = 'https://www.baidu.com'
headers = {'user-agent':'Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10_6_8; en-us) AppleWebKit/534.50 (KHTML, like Gecko) Version/5.1 Safari/534.50'}
r = requests.get(url, headers=headers)
```
## 1.2 正则表达式

### 1.2.1 爬虫任务

结合requests、re两者的内容爬取 https://movie.douban.com/top250 中的内容，要求抓取名次、影片名称、年份、导演等字段。

步骤：

1. 直接进入[https://movie.douban.com/top250](https://movie.douban.com/top250)，观察展示的效果

![](/images/20190407/豆瓣.png)
可以看到名次、影片名称、年份、导演、主演、评分等信息。第一页展示了25个影片信息。点击下一页看到又展示了25个影片信息。还发现网站链接变成了[https://movie.douban.com/top250?start=25&filter=](https://movie.douban.com/top250?start=25&filter=)，多点击几页我们可以发现`start`参数是用来控制返回电影信息的偏移量的，为了获取250个影片信息，可以通过设置`start`，多次访问豆瓣来获取。

2. 利用requests获取返回的信息，打印信息，找到对应的名次、影片名称、年份、导演、主演、评分等字段。
```python
import requests
import re
response = requests.get('https://movie.douban.com/top250')
text, status_code = response.text, response.status_code
text
```
打印部分信息如下：

```
<!DOCTYPE html>\n<html lang="zh-cmn-Hans" class="">\n<head>\n    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">\n    <meta name="renderer" content="webkit">\n    <meta name="referrer" content="always">\n    <meta name="google-site-verification" content="ok0wCgT20tBBgo9_zat2iAcimtN4Ftf5ccsh092Xeyw" />\n    <title>\n豆瓣电影 Top 250\n</title>\n    \n    <meta name="baidu-site-verification" content="cZdR4xxR7RxmM4zE" />\n    <meta http-equiv="Pragma" content="no-cache">\n    <meta http-equiv="Expires" content="Sun, 6 Mar 2005 01:00:00 GMT">\n    \n    <link rel="apple-touch-icon" href="https://img3.doubanio.com/f/movie/d59b2715fdea4968a450ee5f6c95c7d7a2030065/pics/movie/apple-touch-icon.png">\n    <link href="https://img3.doubanio.com/f/shire/bf61b1fa02f564a4a8f809da7c7179b883a56146/css/douban.css" rel="stylesheet" type="text/css">\n    <link href="https://img3.doubanio.com/f/shire/ae3f5a3e3085968370b1fc63afcecb22d3284848/css/separation/_all.css" rel="stylesheet" type="text/css">\n    <link href="https://img3.doubanio.com/f/movie/8864d3756094f5272d3c93e30ee2e324665855b0/css/movie/base/init.css" rel="stylesheet">\n    <script type="text/javascript">var _head_start = new Date();</script>\n    <script type="text/javascript" src="https://img3.doubanio.com/f/movie/0495cb173e298c28593766009c7b0a953246c5b5/js/movie/lib/jquery.js"></script>\n    <script type="text/javascript" src="https://img3.doubanio.com/f/shire/c7db1e57a6f6aebaa1d8ca83a62a94904c19df95/js/douban.js"></script>\n    <script type="text/javascript" src="https://img3.doubanio.com/f/shire/0efdc63b77f895eaf85281fb0e44d435c6239a3f/js/separation/_all.js"></script>\n    \n<link href="https://img3.doubanio.com/f/movie/2c95f768ea74284b900c04c0209b0a44f0a0de52/css/movie/top_movies.css" rel="stylesheet" type="text/css" />\n<script type="text/javascript" src="https://img3.doubanio.com/f/shire/77323ae72a612bba8b65f845491513ff3329b1bb/js/do.js" data-cfg-autoload="false"></script>\n<script type=\'text/javascript\'>\n    Do.ready(function(){\n            $("#mine-selector input[type=\'checkbox\']").click(function(){\n                var val = $(this).is(":checked")?$(this).val():"";\n                window.location.href = \'/top250?filter=\' + val;\n            })\n    })\n</script>\n\n    <style type="text/css">\n.site-nav-logo img{margin-bottom:0;}\n</style>\n    <style type="text/css">img { max-width: 100%; }</style>\n    <script type="text/javascript"></script>\n    <link rel="stylesheet" href="https://img3.doubanio.com/misc/mixed_static/562925b5e3824700.css">\n\n    <link rel="shortcut icon" href="https://img3.doubanio.com/favicon.ico" type="image/x-icon">\n</head>\n\n<body>\n  \n    <script type="text/javascript">var _body_start = new Date();</script>\n\n    \n    \n\n\n\n    <link href="//img3.doubanio.com/dae/accounts/resources/0246c88/shire/bundle.css" rel="stylesheet" type="text/css">\n\n\n\n<div id="db-global-nav" class="global-nav">\n  <div class="bd">\n    \n<div class="top-nav-info">\n  <a href="https://accounts.douban.com/passport/login?source=movie" class="nav-login" rel="nofollow">登录/注册</a>\n</div>\n\n\n    <div class="top-nav-doubanapp">\n  <a href="https://www.douban.com/doubanapp/app?channel=top-nav" class="lnk-doubanapp">下载豆瓣客户端</a>\n  <div id="doubanapp-tip">\n    <a href="https://www.douban.com/doubanapp/app?channel=qipao" class="tip-link">豆瓣 <span class="version">6.0</span> 全新发布</a>\n    <a href="javascript: void 0;" class="tip-close">×</a>\n  </div>\n  <div id="top-nav-appintro" class="more-items">\n    <p class="appintro-title">豆瓣</p>\n    <p class="qrcode">扫码直接下载</p>\n    <div class="download">\n      <a href="https://www.douban.com/doubanapp/redirect?channel=top-nav&direct_dl=1&download=iOS">iPhone</a>\n      <span>·</span>\n      <a href="https://www.douban.com/doubanapp/redirect?channel=top-nav&direct_dl=1&download=Android" class="download-android">Android</a>\n    </div>\n  </div>\n</div>\n\n    \n\n\n<div class="global-nav-items">\n  <ul>\n    <li class="">\n      <a href="https://www.douban.com" target="_blank" data-moreurl-dict="{&quot;from&quot;:&quot;top-nav-click-main&quot;,&quot;uid&quot;:&quot;0&quot;}">豆瓣</a>\n    </li>\n    <li class="">\n      <a href="https://book.douban.com" target="_blank" data-moreurl-dict="{&quot;from&quot;:&quot;top-nav-click-book&quot;,&quot;uid&quot;:&quot;0&quot;}">读书</a>\n    </li>\n    <li class="on">\n      <a href="https://movie.douban.com"  data-moreurl-dict="{&quot;from&quot;:&quot;top-nav-click-movie&quot;,&quot;uid&quot;:&quot;0&quot;}">电影</a>\n    </li>\n    <li class="">\n      <a href="https://music.douban.com" target="_blank" data-moreurl-dict="{&quot;from&quot;:&quot;top-nav-click-music&quot;,&quot;uid&quot;:&quot;0&quot;}">音乐</a>\n    </li>\n    <li class="">\n      <a href="https://www.douban.com/location" target="_blank" data-moreurl-dict="{&quot;from&quot;:&quot;top-nav-click-location&quot;,&quot;uid&quot;:&quot;0&quot;}">同城</a>\n    </li>\n    <li class="">\n      <a href="https://www.douban.com/group" target="_blank" data-moreurl-dict="{&quot;from&quot;:&quot;top-nav-click-group&quot;,&quot;uid&quot;:&quot;0&quot;}">小组</a>\n    </li>\n    <li class="">\n      <a href="https://read.douban.com&#47;?dcs=top-nav&amp;dcm=douban" target="_blank" data-moreurl-dict="{&quot;from&quot;:&quot;top-nav-click-read&quot;,&quot;uid&quot;:&quot;0&quot;}">阅读</a>\n    </li>\n    <li class="">\n      <a href="https://douban.fm&#47;?from_=shire_top_nav" target="_blank" data-moreurl-dict="{&quot;from&quot;:&quot;top-nav-click-fm&quot;,&quot;uid&quot;:&quot;0&quot;}">FM</a>\n    </li>\n    <li class="">\n      <a href="https://time.douban.com&#47;?dt_time_source=douban-web_top_nav" target="_blank" data-moreurl-dict="{&quot;from&quot;:&quot;top-nav-click-time&quot;,&quot;uid&quot;:&quot;0&quot;}">时间</a>\n    </li>\n    <li class="">\n      <a href="https://market.douban.com&#47;?utm_campaign=douban_top_nav&amp;utm_source=douban&amp;utm_medium=pc_web" target="_blank" data-moreurl-dict="{&quot;from&quot;:&quot;top-nav-click-market&quot;,&quot;uid&quot;:&quot;0&quot;}">豆品</a>\n    </li>\n    <li>\n      <a href="#more" class="bn-more"><span>更多</span></a>\n      <div class="more-items">\n        <table cellpadding="0" cellspacing="0">\n          <tbody>\n            <tr>\n              <td>\n                <a href="https://ypy.douban.com" target="_blank" data-moreurl-dict="{&quot;from&quot;:&quot;top-nav-click-ypy&quot;,&quot;uid&quot;:&quot;0&quot;}">豆瓣摄影</a>\n              </td>\n            </tr>\n          </tbody>\n        </table>\n      </div>\n    </li>\n  </ul>\n</div>\n\n  </div>\n</div>\n<script>\n  ;window._GLOBAL_NAV = {\n    DOUBAN_URL: "https://www.douban.com",\n    N_NEW_NOTIS: 0,\n    N_NEW_DOUMAIL: 0\n  };\n</script>\n\n\n\n    <script src="//img3.doubanio.com/dae/accounts/resources/0246c88/shire/bundle.js" defer="defer"></script>\n\n\n\n\n    \n\n\n\n    <link href="//img3.doubanio.com/dae/accounts/resources/0246c88/movie/bundle.css" rel="stylesheet" type="text/css">\n\n\n\n\n<div id="db-nav-movie" class="nav">\n  <div class="nav-wrap">\n  <div class="nav-primary">\n    <div class="nav-logo">\n      <a href="https:&#47;&#47;movie.douban.com">豆瓣电影</a>\n    </div>\n    <div class="nav-search">\n      <form action="https:&#47;&#47;movie.douban.com/subject_search" method="get">\n        <fieldset>\n          <legend>搜索：</legend>\n          <label for="inp-query">\n          </label>\n          <div class="inp"><input id="inp-query" name="search_text" size="22" maxlength="60" placeholder="搜索电影、电视剧、综艺、影人" value=""></div>\n          <div class="inp-btn"><input type="submit" value="搜索"></div>\n          <input type="hidden" name="cat" value="1002" />\n        </fieldset>\n      </form>\n    </div>\n  </div>\n  </div>\n  <div class="nav-secondary">\n    \n\n<div class="nav-items">\n  <ul>\n    <li    ><a href="https://movie.douban.com/cinema/nowplaying/"\n     >影讯&购票</a>\n    </li>\n    <li    ><a href="https://movie.douban.com/explore"\n     >选电影</a>\n    </li>\n    <li    ><a href="https://movie.douban.com/tv/"\n     >电视剧</a>\n    </li>\n    <li    ><a href="https://movie.douban.com/chart"\n     >排行榜</a>\n    </li>\n    <li    ><a href="https://movie.douban.com/tag/"\n     >分类</a>\n    </li>\n    <li    ><a href="https://movie.douban.com/review/best/"\n     >影评</a>\n    </li>\n    <li    ><a href="https://movie.douban.com/annual/2018?source=navigation"\n     >2018年度榜单</a>\n    </li>\n    <li    ><a href="https://www.douban.com/standbyme/2018?source=navigation"\n     >2018书影音报告</a>\n    </li>\n  </ul>\n</div>\n\n    <a href="https://movie.douban.com/annual/2018?source=movie_navigation" class="movieannual2018"></a>\n  </div>\n</div>\n\n<script id="suggResult" type="text/x-jquery-tmpl">\n  <li data-link="{{= url}}">\n            <a href="{{= url}}" onclick="moreurl(this, {from:\'movie_search_sugg\', query:\'{{= keyword }}\', subject_id:\'{{= id}}\', i: \'{{= index}}\', type: \'{{= type}}\'})">\n            <img src="{{= img}}" width="40" />\n            <p>\n                <em>{{= title}}</em>\n                {{if year}}\n                    <span>{{= year}}</span>\n                {{/if}}\n                {{if sub_title}}\n                    <br /><span>{{= sub_title}}</span>\n                {{/if}}\n                {{if address}}\n                    <br /><span>{{= address}}</span>\n                {{/if}}\n                {{if episode}}\n                    {{if episode=="unknow"}}\n                        <br /><span>集数未知</span>\n                    {{else}}\n                        <br /><span>共{{= episode}}集</span>\n                    {{/if}}\n                {{/if}}\n            </p>\n        </a>\n        </li>\n  </script>\n\n\n\n\n    <script src="//img3.doubanio.com/dae/accounts/resources/0246c88/movie/bundle.js" defer="defer"></script>\n\n\n\n\n\n    \n    <div id="wrapper">\n        \n\n        \n    <div id="content">\n        \n    <h1>豆瓣电影 Top 250</h1>\n\n        <div class="grid-16-8 clearfix">\n            \n            \n            <div class="article">\n                \n\n\n\n\n\n\n\n<div class="opt mod">\n    <div class="tabs">\n      \n    \n\n    </div>\n    <span id="mine-selector">\n      <input type="checkbox"  value="unwatched">我没看过的\n    </span>\n</div>\n\n\n\n<ol class="grid_view">\n        <li>\n            <div class="item">\n                <div class="pic">\n                    <em class="">1</em>\n                    <a href="https://movie.douban.com/subject/1292052/">\n                        <img width="100" alt="肖申克的救赎" src="https://img3.doubanio.com/view/photo/s_ratio_poster/public/p480747492.jpg" class="">\n                    </a>\n                </div>\n                <div class="info">\n                    <div class="hd">\n                        <a href="https://movie.douban.com/subject/1292052/" class="">\n                            <span class="title">肖申克的救赎</span>\n                                    <span class="title">&nbsp;/&nbsp;The Shawshank Redemption</span>\n                                <span class="other">&nbsp;/&nbsp;月黑高飞(港)  /  刺激1995(台)</span>\n                        </a>\n\n\n                            <span class="playable">[可播放]</span>\n                    </div>\n                    <div class="bd">\n                        <p class="">\n                            导演: 弗兰克·德拉邦特 Frank Darabont&nbsp;&nbsp;&nbsp;主演: 蒂姆·罗宾斯 Tim Robbins /...<br>\n                            1994&nbsp;/&nbsp;美国&nbsp;/&nbsp;犯罪 剧情\n                        </p>\n\n                        \n                        <div class="star">\n                                <span class="rating5-t"></span>\n                                <span class="rating_num" property="v:average">9.6</span>\n                                <span property="v:best" content="10.0"></span>\n                                <span>1382990人评价</span>\n                        </div>\n\n                            <p class="quote">\n                                <span class="inq">希望让人自由。</span>\n
```
3. 解析需要的字段信息。

完整代码如下：

```python
import requests
import re
import pandas as pd

def access_douban(start):
    '''
    访问豆瓣网，获取top250影片中的25个电影信息，从start开始计数
    '''
    headers = {'user-agent':'Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10_6_8; en-us) AppleWebKit/534.50 (KHTML, like Gecko) Version/5.1 Safari/534.50',}
    params = {'start':start}
    try:
        response = requests.get('https://movie.douban.com/top250', params=params, headers=headers)
        return response
    except Exception as e:
        print(e)
        return None

### 每一部电影的信息
single_film_pattern = re.compile('<div class="item">(.*?)</p>\n                    </div>\n                </div>\n            </div>', re.S)
rank_pattern = re.compile('<em class="">(\\d+)</em>', re.S) #排名
film_name_pattern = re.compile('<span class="title">(.*?)</span>', re.S) #多个电影名称
other_name_pattern = re.compile('<span class="other">(.*?)</span>', re.S) #其他电影名称
director_actor_pattern = re.compile('<p class="">(.*?)</p>', re.S) # 导演、主演、年份
score_pattern = re.compile('<span class="rating_num" property="v:average">(.*?)</span>', re.S) #得分
one_space_pattern = re.compile('&nbsp;', re.S) #一个空格
three_space_pattern = re.compile('&nbsp;&nbsp;&nbsp;', re.S) #三个空格

### 解析电影信息
ranks = []
film_names = []
directors = []
actors = []
years = []
scores = []
for i in range(10):
    start = i * 25
    response = access_douban(start)
    if response is not None and response.status_code == 200:
        result = single_film_pattern.findall(response.text)
        if len(result) > 0:
            for single_film in result:
                rank = int(rank_pattern.findall(single_film)[0])
                film_names1 = film_name_pattern.findall(single_film)
                film_names2 = other_name_pattern.findall(single_film)
                director_actor_year_info = director_actor_pattern.findall(single_film)[0].strip().split('<br>\n')
                director_actor = director_actor_year_info[0].split('&nbsp;&nbsp;&nbsp;')
                director = director_actor[0].split(':')[-1].strip()
                if len(director_actor) > 1:
                    actor = director_actor[1].split(':')[-1].strip()
                else: actor = ''
                year = director_actor_year_info[1].split('&nbsp;')[0].strip()
                score = float(score_pattern.findall(single_film)[0])
                film_names1.extend(film_names2)
                film_name = '/'.join([film_name.strip() for film_name in one_space_pattern.sub('', ''.join(film_names1)).split('/')])
                ranks.append(rank)
                film_names.append(film_name)
                years.append(year)
                directors.append(director)
                actors.append(actor)
                scores.append(score)

### 保存电影信息
data = pd.DataFrame({'排名': ranks, '电影名称': film_names, '导演': directors, '主演': actors, '年份': years, '得分': scores})
data.to_excel('豆瓣top250.xlsx', index=False)
```




## 参考链接
1. [常见的响应状态码](https://www.jianshu.com/p/e358607a3e1b)
2. [百度百科](https://baike.baidu.com/item/http%E8%AF%B7%E6%B1%82%E5%A4%B4/6623287?fr=aladdin)
3. [常用的HTTP请求头与响应头](https://blog.csdn.net/qq_30553235/article/details/79282113)
