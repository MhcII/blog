---
title: 解决Vultr Ubuntu16.04.1 装 Apache 后外网无法访问
date: 2019-04-08 11:44:10
tags:
---

# 发现问题
前一段时间在 Vultr 的 VPS 上装了 Apache 后，发现无法访问。想到以下几种可能

- Apache 没有安装成功

  在服务器上用 w3m 发现是可以访问服务器的。排除

- Apache 配置只能在本地访问

  修改配置文件，使用 `netstat -anp | grep 80` 命令查看 80 端口的监听。仍然没问题。排除

- Vultr 被 GFW 了，在中国不能访问

  ping 服务器的 IP 地址，可以 ping 通。排除

- 防火墙隔离了 80 端口

  使用 [端口扫描](http://tool.chinaz.com/port/) 查看服务器的端口是否开放，发现 80 端口确实是关闭状态，应该是防火墙或者 Vultr 的网络服务问题。

  查询 Vultr 的文档，[Install Wordpress with Apache, PHP and MySQL (Automated Startup Script)](https://www.vultr.com/docs/install-wordpress-with-apache-php-and-mysql-automated-startup-script)。发现其中有如下一段。

  ![](3120472-d6600678e8c07999.png)

  找到原因了，确实是防火墙没有开放80端口

# 解决

按照文档输入了如下配置

```shell
iptables -F
iptables -A INPUT -i lo -j ACCEPT
iptables -A INPUT -p tcp -m tcp --dport 22 -j ACCEPT
iptables -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
iptables -A INPUT -p tcp -m tcp --dport 443 -j ACCEPT
iptables -A INPUT -p tcp -m tcp --dport 8000 -j ACCEPT
```

发现外网可以访问服务器了。。

***

> 原文地址：[解决Vultr Ubuntu16.04.1 装 Apache 后外网无法访问](https://blog.mhcii.cn/blog/develop/fix-vultr-install-apache-cannot-visit.html)
>
> 转载请注明出处

