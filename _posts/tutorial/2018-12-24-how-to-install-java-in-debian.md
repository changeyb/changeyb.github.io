---
layout: post
title:  "如何在debian 8上安装java 8"
categories: 教程
tags:  debian jdk安装
author: Benjamin
---

* content
{:toc}

具体步骤如下：




1. 进入或创建一个你希望安装java的文件夹your_software_dir。通过如下命令下载jdk：

`wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" https://download.oracle.com/otn-pub/java/jdk/8u191-b12/2787e4a523244c269598db4e85c51e0c/jdk-8u191-linux-x64.tar.gz`

2. 解压文件 `tar -zxvf jdk-8u191-linux-x64.tar.gz`

3. 配置java环境变量
  * vim /etc/profile
  * 将下面内容复制到底部：
  ```sh
  JAVA_HOME=your_software_dir/jdk1.8.0_191
  PATH=$JAVA_HOME/bin:$PATH
  export PATH JAVA_HOME
  ```
  * `:wq`保存文件
  * 使用命令`source /etc/profile`使配置生效

4. `java -version`验证是否安装成功
