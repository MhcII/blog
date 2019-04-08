---
title: Win10 安装 LAMP
date: 2019-04-08 11:44:10
tags:
---

# 安装 [PHP 7.1.0](http://windows.php.net/download#php-7.1)

1. 下载 [PHP 7.1.0](http://windows.php.net/download#php-7.1)

   我选择的版本是 VC14 x64 Thread Safe

2. 下载后解压到要安装的位置

   我安装在 `D:\develop\php\php-7.1.0`

3. 将 `php.ini-development` 复制一份命名为 `php.ini`

4. 修改 `php.ini` 

5. 找到 On windows 的 `extension_dir` 这一行，去掉注释，修改为 

   ```ini
   extension_dir = "D:\Developer\PHP\PHP-Ts\ext"
   ```

6. 去掉以下扩展的注释

   ```ini
   php_curl
   php_gd2
   php_mysqli
   php_pdo_mysql
   php_mbstring
   ```

7. 把PHP的路径加入系统环境变量中

# 安装 [Apache 2.4.25](http://www.apachehaus.com/cgi-bin/download.plx)

1. 下载 [Apache 2.4.25](http://www.apachehaus.com/cgi-bin/download.plx) 。

   我选择的版本是 vc14 x64版本的。

2. 下载后解压到想要安装的位置

   我安装在 `D:\develop\apache\Apache-2.4.25` 。

3. 修改目录下 `conf\httpd.conf` 修改配置

4. `Define SRVROOT` 修改为 `Define SRVROOT "D:/Developer/Apache/Apache24"`    

5. `Define SRVROOT` 在后面增加一行 `Define WEBROOT "E:/Work/WorkSpace/www"`

   这个就是你的 `www` 目录的路径

6. 修改 `DocumentRoot` 为 `DocumentRoot "${WEBROOT}"`

   修改下面的 `<Directory "${SRVROOT}/htdocs">` 为 `<Directory "${WEBROOT}">`

   `AllowOverride None` 修改为 `AllowOverride All`

7. 然后在CMD管理员权限中输入以下命令

   ```shell
   cd /d D:\Developer\Apache\Apache24\bin
   httpd -k install
   ```

   此时访问 `localhost` 能访问网站说明安装成功了。

8. 启用PHP支持

9. 修改 `conf\httpd.conf` 在最后一个 `LoadModule` 下增加

   ```
   # PHP7 Config
   LoadModule php7_module "D:/Developer/PHP/PHP-Ts/php7apache2_4.dll"
   PHPIniDir "D:/Developer/PHP/PHP-Ts"
   AddType application/x-httpd-php .php .html .htm
   ```

10. 重启Apache

***

> 原文地址：[Win10 安装 LAMP](https://blog.mhcii.cn/blog/develop/install-lamp-in-win10.html)
>
> 转载请注明出处

