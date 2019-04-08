---
title: Ubuntu 16 安装 Laravel 开发环境
date: 2019-04-08 11:44:10
tags:
---

此文甚是详细，刚接触 Linux 的人也可以操作。

# 安装 LAME
这些是最基本的开发 Php 需要的软件

## 1. 安装前先更新系统

```shell
# 在终端中执行
sudo apt-get update
sudo apt-get upgrade
```
如果你不知道怎么打开终端，在 Ubuntu 按下 `Win键` 可以进入搜索（如果你不知道这个按键是哪个，去百度一下），在最上面搜索条里输入 `z` ，第一个搜到的应该就是终端，如果没有，输入 `终端` 就能找到了。

## 2. 安装Apache
```shell
# 在终端中执行
sudo apt-get install apache2
sudo a2enmod rewrite
```
测试 Apache 是否安装成功，在浏览器输入 `http://localhost/` 看看是否能打开网页。显示出来的是个 Apache的欢迎页面。
```shell
# 一些Apache命令
# 启动 
sudo service apache2 start
# 重启
sudo service apache2 restart
# 关闭 
sudo service apache2 stop
```
## 3. 安装Php（Php7.0）
```shell
# 在终端中执行
sudo apt-get install php
sudo apt-get install libapache2-mod-php php-zip php-mysql php-mbstring php-gettext
```
测试 Php 是否安装成功，如果安装成功，不需要重启系统就能用了。 Apache 的默认 www 目录在 `/var/www/html/`，在此目录下建立一个 `PhpInfo.php` ，测试一下 Php 是否安装成功，方法如下：
> 先说一下 Vim 怎么用
>
> 首先如果没装 Vim 的话，装一个 Vim
>
> ```shell
> # 在终端中执行
> sudo apt-get install vim
> ```
>
> 在 Vim 窗口中按下 `i` 可以进入编辑模式，按下 `Esc` 可以退出编辑模式。
>
> 在非编辑模式输入`:` 可以输入一些指令。 `:wq`  是保存并退出。
1. 创建 `PhpInfo.php` 文件

   ```shell
   # 在终端中执行
   sudo vim /var/www/html/PhpInfo.php
   ```

2. 在Vim窗口中按 `i` 进入编辑模式，然后输入以下内容

   ```php
   # 在Vim中输入
   <?php phpinfo(); ?>
   ```

3. 按 `Esc` 退出编辑模式，输入 `:wq` 保存并退出。

此时打开 `http://localhost/PhpInfo.php` ，看看是不是出现了有关Php的信息。如果出现了就是安装成功了。
这个PhpInfo.php不要删除，一会还有用处。
## 4. 安装MySql
```shell
# 在终端中执行
sudo apt-get install mysql-server mysql-client
```
中间会让你设置一下root用户的密码。
## 5. 安装PhpMyAdmin
```shell
# 在终端中执行
sudo apt-get install phpmyadmin
sudo ln -s /usr/share/phpmyadmin /var/www/html/PhpMyAdmin
```
安装后重启一下Apache，命令是 `sudo /etc/init.d/apache2 restart` 。然后进入 `http://localhost/PhpMyAdmin/` 看是否能打开PhpMyAdmin。
## 6. 安装Composer
```shell
# 在终端中执行
cd ~
sudo php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
sudo php composer-setup.php
sudo mv composer.phar /usr/local/bin/composer
sudo php -r "unlink('composer-setup.php');"
```
测试是否安装成功（我写这个笔记时候不需要搭梯子就能连接Composer），**这个测试很浪费时间，一般不必执行**。
```shell
# 在终端中执行
cd /var/www/html/
composer global require "laravel/installer"
sudo ~/.composer/vendor/bin/laravel new Test
sudo chmod -R 777 Test/
```
安装很费时，你可以去干点别的。安装结束后，会在你的 `/var/www/html/` 目录下增加一个名为 `Test` 的Laravel项目，然后浏览器打开 `http://localhost/Test/public/` 看看是否进入了一个主页。
## 7. 安装PhpStorm
PhpStorm是[JetBrains](https://www.jetbrains.com/)公司的一款用于编辑Php的Ide。JetBrains公司的产品都不错，推荐大家使用。

1. 下载PhpStorm，[点此下载PhpStorm](https://www.jetbrains.com/phpstorm/download/#section=linux-version)。可以试用30天，或者自己百度激活。
2. 下载完成后，在文件管理器里找到下载到的文件，在终端中输入

```shell
# 在终端中执行
cd ~/下载
tar xvf [下载的PhpStorm文件名]
sudo mv [解压后的文件夹] /opt/PhpStorm/
sudo ln -s /opt/PhpStorm/bin/phpstorm.sh /usr/local/bin/PhpStorm
PhpStorm
```

如果打开 PhpStorm 无误，那么安装成功，可以开始开发啦！

***

> 参考文章
>
> 1. [Ubuntu 16.04 安装 Apache, MySQL, PHP7](https://www.cnblogs.com/2016xt/p/5517049.html) 2016-05-22
> 2. [linux 下 apache启动、停止、重启命令](http://blog.sina.com.cn/s/blog_70ac6bec01018mqs.html) 2012-11-22
> 3. [Ubuntu14.04下安装Composer](http://www.07net01.com/2015/10/938199.html) 2015-10-08
> 4. [在Ubuntu系统下安装PhpStorm并启动的方法](http://www.linuxdiyf.com/linux/19328.html) 2016-03-28

***

> 原文地址：[Ubuntu 16 安装 Laravel 开发环境](https://blog.mhcii.cn/blog/develop/install-laravel-on-ubuntu.html)
>
> 转载请注明出处

