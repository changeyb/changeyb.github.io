---
layout: post
title:  "心率恢复率"
categories: 健身
tags: 心率 恢复率
author: Benjamin
---

* content
{:toc}

心率恢复率，即运动后心率恢复到正常水平的速率。心率恢复率的大小一定程度上反映了一个人的健康程度。如何测量心率恢复率呢？主要分为3步：


## 第一步：找到目标心率

下面的表格是各个年龄段的目标心率：
* 20-29: 120-160 bpm
* 30-39: 114-152 bpm
* 40-49: 108-144 bpm
* 50-59: 102-136 bpm
* 60-69: 96-128 bpm
* 70-79: 90-120 bpm
* 80-89: 84-112 bpm
* 90-99: 78-104 bpm
* 100以上: 72-96 bpm

上面的目标心率是用最大心率（220 - 年龄）的60%～80%估计出来的。

目标心率的计算方式也有说法是：（最大心率 - 安静心率）* 60%～80% + 安静心率

## 第二步：进行运动项目

进行运动项目，如跑步，骑车，踏板测试等，使的心率在目标心率区间。停止运动，记录下2个指标：
1. 立即停止运动后的心率$rate_1$
2. 停止运动2分钟后的心率$rate_2$

## 第三步： 计算心率恢复率

$心率恢复率=rate_1-rate_2$,这个值越大，代表心脏越健康。

心率恢复率即健康程度的参考数据如下：
* <22: 身体年龄略大于真实年龄
* 22～52: 身体年龄=真实年龄
* 53～58: 身体年龄略小于真实年龄
* 59～65: 身体年龄比真实年龄小
* >=66: 身体年龄比真实年龄小很多





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
  摘取打印出的部分信息如下：
  ```<div class="item">\n                <div class="pic">\n                    <em class="">1</em>\n                    <a href="https://movie.douban.com/subject/1292052/">\n                        <img width="100" alt="肖申克的救赎" src="https://img3.doubanio.com/view/photo/s_ratio_poster/public/p480747492.jpg" class="">\n                    </a>\n                </div>\n                <div class="info">\n                    <div class="hd">\n                        <a href="https://movie.douban.com/subject/1292052/" class="">\n                            <span class="title">肖申克的救赎</span>\n                                    <span class="title">&nbsp;/&nbsp;The Shawshank Redemption</span>\n                                <span class="other">&nbsp;/&nbsp;月黑高飞(港)  /  刺激1995(台)</span>\n                        </a>\n\n\n                            <span class="playable">[可播放]</span>\n                    </div>\n                    <div class="bd">\n                        <p class="">\n                            导演: 弗兰克·德拉邦特 Frank Darabont&nbsp;&nbsp;&nbsp;主演: 蒂姆·罗宾斯 Tim Robbins /...<br>\n                            1994&nbsp;/&nbsp;美国&nbsp;/&nbsp;犯罪 剧情\n                        </p>\n\n                        \n                        <div class="star">\n                                <span class="rating5-t"></span>\n                                <span class="rating_num" property="v:average">9.6</span>\n                                <span property="v:best" content="10.0"></span>\n                                <span>1382990人评价</span>\n                        </div>\n\n                            <p class="quote">\n                                <span class="inq">希望让人自由。</span>\n
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
single_film_pattern = re.compile('<div class="item">(.*?)\s+</div>\s+</div>\s+</div>', re.S)
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
