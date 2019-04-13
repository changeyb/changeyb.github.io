---
layout: post
title:  "爬虫任务四"
categories: crawl
tags: crawl 爬虫
author: Benjamin
---

* content
{:toc}

加入DataWhale爬虫学习群，通过做任务的方式初步了解爬虫技术。




##  实战大项目

模拟登录丁香园，并抓取论坛页面所有的人员基本信息与回复帖子内容


具体代码如下：

```Python
import requests
from selenium import webdriver
from webdriver_manager.chrome import ChromeDriverManager
from lxml import etree
import pandas as pd

headers = {'user-agent':'Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10_6_8; en-us) AppleWebKit/534.50 (KHTML, like Gecko) Version/5.1 Safari/534.50'}
url = 'http://www.dxy.cn/bbs/thread/626626#626626'
user = '17771849047'
passwd = '87e6kTCrapPgw4F'
browser = webdriver.Chrome(ChromeDriverManager().install())
browser.get(url)
login = browser.find_element_by_link_text('登录')
login.click()
browser.refresh()
reback_computer = browser.find_element_by_partial_link_text('返回电脑')
reback_computer.click()
user_ele = browser.find_element_by_name('username')
passwd_ele = browser.find_element_by_name('password')
button = browser.find_element_by_xpath('//button[@class="button"]')
user_ele.clear()
passwd_ele.clear()
user_ele.send_keys(user)
passwd_ele.send_keys(passwd)
button.click()
link_a = browser.find_elements_by_xpath('//div[@class="avatar128"]/span/a')
for a in link_a:
    actions = ActionChains(browser)
    actions.move_to_element(a)
    actions.perform()

r = etree.HTML(browser.page_source)
postcontainer = r.xpath('//div[@id="postcontainer"]')
posts = postcontainer[0].xpath('child::div')
post_data = []
for post in posts:
    personMsgDialog_list = post.xpath('descendant::div[@id="personMsgDialog"]')
    if len(personMsgDialog_list) > 0:
        print(personMsgDialog_list)
        personMsgDialog = personMsgDialog_list[0]
        print(personMsgDialog.xpath('descendant::span[@class="nickname"]'))
        nickname = personMsgDialog.xpath('descendant::span[@class="nickname"]')[0].text
        statusTitle = personMsgDialog.xpath('descendant::span[@class="statusTitle"]')[0].text
        posts_ = personMsgDialog.xpath('descendant::span[@class="posts"]')[0].text
        distilled = personMsgDialog.xpath('descendant::span[@class="distilled"]')[0].text
        votes = personMsgDialog.xpath('descendant::span[@class="votes"]')[0].text
        score = personMsgDialog.xpath('descendant::span[@class="score"]')[0].text
        money = personMsgDialog.xpath('descendant::span[@class="money"]')[0].text
        follower = personMsgDialog.xpath('descendant::span[@class="follower"]')[0].text
        lastLoginTime = personMsgDialog.xpath('descendant::span[@class="lastLoginTime"]')[0].text
    else:
        nickname = post.xpath('descendant::div[@class="auth"]/a/text()')[0]
        statusTitle = None
        posts_ = None
        distilled = None
        votes = None
        score = None
        money = None
        follower = None
        lastLoginTime = None
    postbody = post.xpath('descendant::td[@class="postbody"]')[0]
    postmessage = ''.join(postbody.xpath('descendant::text()')).strip()
    x = pd.Series([nickname, statusTitle, posts_, distilled, votes, score, money, follower, lastLoginTime, postmessage], index=['名称', '级别', '帖子', '精华', '得票', '得分', '丁当', '粉丝', '最后登录', '回复'])
    post_data.append(x)
pd.DataFrame(post_data)  
```

数据如下：

![](/images/20190413/丁香园.png)

## 待解决问题：
1. 验证码问题
2. 获取用户详细信息
