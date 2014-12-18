---
layout:         post
title:         Ubuntu基础环境搭建
description: 本篇介绍Ubuntu基础环境搭建
keywords: Unix, Linux, Ubuntu
category: Unix
tags: [Unix,Linux,Ubuntu]
---

本文基于Ubuntu12.04，阐述基础环境搭建过程：JDK+Nginx+Tomcat+Redis+PostgreSQL。

####JDK安装

* 1.在线安装

{% highlight sh %}
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java7-installer
sudo apt-get install oracle-java7-set-default
{% endhighlight %}
