---
layout: post
title:  "爬虫任务二"
categories: crawl
tags: crawl 爬虫 BeautifulSoup
author: Benjamin
---

* content
{:toc}

加入DataWhale爬虫学习群，通过做任务的方式初步了解爬虫技术。




## 1.1 学习BeautifulSoup， 利用BeautifulSoup提取内容

### 1.1.1 初步了解BeautifulSoup
Beautiful Soup 是一个可以从HTML或XML文件中提取数据的Python库。可以通过`find_all`方法很方便的找到需要的信息。

### `find_all()`简介

`find_all( name , attrs , recursive , text , **kwargs )`

`find_all()` 方法搜索当前`tag`的所有`tag`子节点,并判断是否符合过滤器的条件.这里有几个例子:
```python
soup.find_all("title")
# [<title>The Dormouse's story</title>]

soup.find_all("p", "title")
# [<p class="title"><b>The Dormouse's story</b></p>]

soup.find_all("a")
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
#  <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>,
#  <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]

soup.find_all(id="link2")
# [<a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>]

import re
soup.find(text=re.compile("sisters"))
# u'Once upon a time there were three little sisters; and their names were\n'
```
由于find_all() 几乎是Beautiful Soup中最常用的搜索方法,Beautiful Soup团队还特意定义了它的简写方法. BeautifulSoup 对象和 tag 对象可以被当作一个方法来使用,这个方法的执行结果与调用这个对象的 find_all() 方法相同,下面两行代码是等价的:

```python
soup.find_all("a")
soup("a")
```
### 1.1.2 使用Beautifulsoup提取丁香园论坛的回复内容

步骤：
1. 打开丁香园论坛[http://www.dxy.cn/bbs/thread/626626#626626](http://www.dxy.cn/bbs/thread/626626#626626)，查看网页源码，找到用户回复的内容，如下图所示：
![](/images/20190409/丁香园.png)

2. 观察到回复内容的标签是`<td class="postbody">`，利用BeautifulSoup和requests提取回复内容。

具体代码如下：
```python
import requests
from bs4 import BeautifulSoup
r = requests.get('http://www.dxy.cn/bbs/thread/626626#626626')
soup = BeautifulSoup(r.text)
[x.text.strip() for x in soup('td', 'postbody')]
```
输出如下：
![](/images/20190409/回复内容.png)

## 1.2 学习xpath，利用lxml和xpath提取内容
### 1.2.1 了解xpath
XPath 使用路径表达式来选取 XML 文档中的节点或节点集。节点是通过沿着路径 (path) 或者步 (steps) 来选取的。

#### 基本语法

选取节点：

| 表达式     | 描述     |
| :------------- | :------------- |
| nodename | 选取此节点的所有子节点 |
| / | 从根节点选取|
| // | 从匹配选择的当前节点选择文档中的节点，而不考虑它们的位置。|
| .   | 选取当前节点 |
| .. | 选取当前节点的父节点。|
| @  | 选取属性 |


谓语：

| 路径表达式 | 结果     |
| :------------- | :------------- |
| /bookstore/book[1]      |选取属于 bookstore 子元素的第一个 book 元素。|
| /bookstore/book[last()]	      |选取属于 bookstore 子元素的最后一个 book 元素。|
|/bookstore/book[last()-1]|选取属于 bookstore 子元素的倒数第二个 book 元素。|
|/bookstore/book[position()<3]|选取最前面的两个属于 bookstore 元素的子元素的 book 元素。|
|//title[@lang]	|选取所有拥有名为 lang 的属性的 title 元素。|
|//title[@lang='eng']	|选取所有 title 元素，且这些元素拥有值为 eng 的 lang 属性。|
|/bookstore/book[price>35.00]	|选取 bookstore 元素的所有 book 元素，且其中的 price 元素的值须大于 35.00|
|/bookstore/book[price>35.00]/title|选取 bookstore 元素中的 book 元素的所有 title 元素，且其中的 price 元素的值须大于 35.00。|

选取未知节点：

| 通配符 | 描述     |
| :------------- | :------------- |
|*|匹配任何元素节点|
|@*|匹配任何属性节点|
|node()|匹配任何类型的节点|

### 1.2.2利用lxml和xpath提取丁香园论坛的回复内容

具体代码如下：
```Python
import requests
from lxml import etree
r = etree.HTML(requests.get('http://www.dxy.cn/bbs/thread/626626#626626').text)
comments = [x for x in r.xpath('//td[@class="postbody"]')]
[''.join(comment.xpath('text()')).strip() for comment in comments]
```
输出如下：
![](/images/20190409/回复内容.png)
**注意：**
如果直接采用`[x for x in r.xpath('//td[@class="postbody"]/text()')]`的方式提取评论，评论数会超过4条。

## 参考链接
1. [Beautiful Soup 4.2.0 文档](https://www.crummy.com/software/BeautifulSoup/bs4/doc/index.zh.html)
2. [xpath菜鸟教程](http://www.runoob.com/xpath/xpath-tutorial.html)
3. [学习xpath，使用lxml+xpath提取内容](https://blog.csdn.net/naonao77/article/details/88129994)
