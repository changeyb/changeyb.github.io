---
layout: post
title:  "爬虫任务三"
categories: crawl
tags: crawl 爬虫 selenium 代理池 ip
author: Benjamin
---

* content
{:toc}

加入DataWhale爬虫学习群，通过做任务的方式初步了解爬虫技术。




## 1.1 安装selenium并学习

### 1.1.1 selenium安装方法

#### selenium安装
`conda install selenium`

#### chromedriver安装
1. `pip install webdriver-manager`
2. `from selenium import webdriver`
`from webdriver_manager.chrome import ChromeDriverManager`
`driver = webdriver.Chrome(ChromeDriverManager().install())`

### 1.1.2 selenium模拟登陆163邮箱

完整代码如下：

```Python
from selenium import webdriver
from webdriver_manager.chrome import ChromeDriverManager
driver = webdriver.Chrome(ChromeDriverManager().install())
driver.get('https://mail.163.com/')
driver.switch_to_frame(0)#找到邮箱账号登录框对应的iframe,由于网页中iframe的id是动态的，所以不能用id寻找
email = driver.find_element_by_name('email')#找到邮箱账号输入框
email.send_keys('your_email@163.com')#将自己的邮箱地址输入到邮箱账号框中
passwd = driver.find_element_by_name('password')
passwd.send_keys('your_passwd')
button = driver.find_element_by_id('dologin')
button.click()
```
## 2.1 学习ip相关知识

### 2.1.1 ip
互联网协议地址，缩写为IP地址，是分配给网络上使用网际协议的设备的数字标签。

### 2.1.2 为什么爬取网站内容时ip会被封？
网站为了防止被爬取，会有反爬机制，对于同一个IP地址的大量同类型的访问，会封锁IP，过一段时间后，才能继续访问。

### 2.1.3 如何应对ip被封
常用方法：
* 修改请求头，模拟浏览器（而不是代码去直接访问）去访问
* 构建ip代理池，轮换访问
* 设置访问时间间隔

### 2.2 爬取西刺代理
代码如下：
```python
import requests
from lxml import etree
headers = {'user-agent':'Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10_6_8; en-us) AppleWebKit/534.50 (KHTML, like Gecko) Version/5.1 Safari/534.50'}
r = requests.get('https://www.xicidaili.com/', headers=headers)
r = etree.HTML(r.text)
trs = r.xpath('//tr')
proxy_ip_list = []
for tr in trs:
    tds = tr.xpath('td')
    if len(tds) == 8:
        ip = tds[1].text
        port = tds[2].text
        protocal = tds[5].text
        if protocal.lower() in ('http', 'https'):
            proxy_ip_list.append(f'{protocal}://{ip}:{port}')
```
爬取的ip类型如下：

![](/images/20190411/代理.png)

## 可能会遇到的问题：
按照通常的方法下载chromedriver，设置环境变量，等到使用的时候还是会报错，报错信息如下：
![](/images/20190410/error.png)
解决方法见参考链接。

## 参考链接
1. [Error message: “'chromedriver' executable needs to be available in the path”](https://stackoverflow.com/questions/29858752/error-message-chromedriver-executable-needs-to-be-available-in-the-path)
2. [selenium参考文档](https://selenium-python.readthedocs.io/api.html)
3. [Python爬虫学习-Day5](https://blog.csdn.net/weixin_42937385/article/details/88150379)
4. [爬虫学习Day6：ip](https://blog.csdn.net/weixin_43720396/article/details/88218204)
