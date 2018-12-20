### mac php 安装


一、启动Apache
有两种方法

1、打开网络共享

   打开"系统偏好设置"->"共享"，在"互联网共享"那一项前面打√。

2、打开终端，输入

sudo apachectl start
这时需要输入密码，输入电脑密码即可,然后输入

sudo apachectl －v
可以查看到Apache的版本信息
Server version: Apache/2.2.24 (Unix)
Server built:   Jul  7 2013 18:05:17
此时在浏览器中输入http://localhost，会出现It works！的页面

二、运行PHP

1. 找到Apache的配置文件，在目录/etc/apache2/下，打开Finder，选择"前往"-"前往文件夹"，输入"/etc/apache2/"，找到其中的"httpd.conf"文件，选择用文稿打开进行编辑，点按Command+F，搜索#LoadModule php5_module libexec/apache2/libphp5.so

2. 重启Apache，在终端输入
 	sudo apachectl restart 
 	
   PHP就可以用了。
3. 在终端输入sudo cp /Library/WebServer/Documents/index.html.en /Library/WebServer/Documents/info.php
即在Apache的根目录下复制index.html.en文件并重命名为info.php。

4. 打开info.php，在It works后面加上<?php phpinfo(); ?>,然后再次重启Apache，在浏览器中输入http://localhost/info.php，会出现一个显示php信息的页面，如图所示。
5. 所有的php文件放在/Library/WebServer/Documents/目录下，并且在浏览器输入http:localhost/php文件所在目录/php文件名  来运行php页面程序；



### mysql 

1. brew install mysql
2. mysql.server start
3. mysqladmin -u root password "123456"
4. mysql -u root -p
5.  mysql_secure_installation



### 链接

[我的总结](https://my.oschina.net/mather/blog/739333)

[官网安装](http://php.net/manual/zh/install.php)

[在Mac下配置php开发环境：Apache+php+MySql](http://my.oschina.net/joanfen/blog/171109)

[masql安装](https://www.jianshu.com/p/e69ddc8a47b7)