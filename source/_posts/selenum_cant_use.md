---
title: Webdriver一次坑爹的体验： Can not connect to the Service chromedriver解决办法
date: 2019-04-08 11:44:10
tags:
---

换了各种配置，selenium 卸载删除了无数遍。各种重装、重配 XXXXX。

最后的最后：hosts 里去少了 

`127.0.0.1 localhost` 这一句！！ 

加上后，解决了问题

***
> 原文地址：[Webdriver一次坑爹的体验： Can not connect to the Service chromedriver解决办法](http://blog.csdn.net/crisschan/article/details/70209909)
转载请注明出处

