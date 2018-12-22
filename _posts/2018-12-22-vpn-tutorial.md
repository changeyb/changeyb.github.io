---
layout: post
title:  "VPN教程"
categories: 教程
tags:  vps linode shadowsocks putty Kcptun 翻墙 工具软件
author: Benjamin
---

* content
{:toc}

这个教程基本上照搬同学发给我的配置教程，目的是半个小时的配置，搭建一个稳定高速的梯子，科学上网。





具体过程如下：

## 1.购买VPS

VPS(Virtual Private Server) 选择很多，这里选择[Linode](https://www.linode.com/)，比起其它厂家，机器配置/流量/带宽/稳定性都会好一点，现在价格也便宜，最基本的配置现在仅需要5$/月。我这里直接按照同学的推荐选择了Fremont, CA, USA节点，速度和延迟都能满足要求。

注册好Linode账号后，选择最便宜的就行了，用来搭梯子完全够用。

之后可以看到购买的机器和它的部分属性，比如IP。

![](images/20181222/Linode.PNG)

## 2.安装Shadowsocks

### 2.1安装Debian

* 点击Dashboard，进入到机器的配置部分
* 选择Deploy an Image
* Image选择Debian 8
* 设置Root密码
* 点击Deploy
* 回到Dashboard页面，等待Host Job Queue跑完之后，点击Boot来启动操作系统

### 2.2安装Shadowsocks

VPS没有图形界面，所有的操作和输出都要通过命令来进行，这里用[PuTTY](https://the.earth.li/~sgtatham/putty/latest/w64/putty-64bit-0.70-installer.msi)来进行。

* 下载PuTTY后，按下图输入VPS的IP，
![](images/20181222/putty.PNG)，
其它保持不变，点击open
* login as:root
* password: Linode配置时设置的Root密码
* 输入 `apt-get install curl`
* 输入 `curl 'https://raw.githubusercontent.com/shadowsocks/stackscript/master/stackscript.sh?v=4' > /tmp/ss.sh && bash /tmp/ss.sh && rm /tmp/ss.sh`，并等待任务完成
* 输入 `supervisorctl status` 检查下Shadowsocks是否已经开始运行，正常情况下会出现 `shadowsocks RUNNING`
* 输入 `cat /etc/shadowsocks.json` 查看Shadowsocks生成的随机配置。例如：
```
{
    "server":"0.0.0.0",
    "server_port":4762,
    "local_port":1080,
    "password":"8d779a1ee2db776db8e20adffaa12d0c",
    "timeout":300,
    "method":"aes-256-cfb"
}
```
### 2.3 客户端（需要翻墙的机器）配置Shadowsocks

* 下载[Shadowsocks](https://github.com/shadowsocks/shadowsocks-windows/releases)
* 下载好Shadowsocks.zip，解压，里面只有一个Shadowsocks.exe。打开，输入自己的服务器ip、端口、密码。

  **注意：** 服务器IP填写Linode服务器的IP，不是前面提到的Shadowsocks生成的 `"server":"0.0.0.0"`，但是服务器端口、密码和加密方式分别对应前面Shadowsocks生成的 **server_port, password, method**。配置好Shadowsocks后，右键Shadowsocks图标，勾选 **启动系统代理**，如下图所示：
  ![](images/20181222/shadow.jpg)
* 此时，电脑已经具备了翻墙能力，直接使用google搜索了。

## 3. Kcptun加速

有追求的孩子可能还不满足于仅仅使用Google, Twitter，想要更进一步，流畅体验油管视频，此时就需要Kcptun 加速了

具体怎么配置Kcptun这里不做赘述，这里参考一下Leonn的博客就够了。
1. [Kcptun服务器配置](https://blog.liyuans.com/archives/kcptun-server-configuration-tutorial.html)
2. [Kcptun客户端配置](https://blog.liyuans.com/archives/kcptun-client-configuration-tutorial.html)

 ## 4. 可能碰到的问题

 1. 能ping通服务器，但客户端还是不能翻墙，有可能是Linode给你分配的ip被墙了，需要重新更换ip。由于Linode是按照使用时常收费的，更换ip比较简单的方式是删除选择的节点，重新选择一个新的服务器，会重新分配一个ip，按照前面提到的配置重新配置一遍，正常来说就可以翻墙了。
