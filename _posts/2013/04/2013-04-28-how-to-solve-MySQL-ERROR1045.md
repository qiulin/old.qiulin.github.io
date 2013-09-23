---
layout: post
title: "如何解决MySQL ERROR1045"
description: "如何解决MySQL Access denied for user \'root\'@\'localhost\'"
modified: 2013-08-20
tags: [MySQL]
image:
  feature: abstract-10.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
comments: true
share: true  
---

很长时间没有登陆过mysql，结果把密码忘记了，一直报MySQL ERROR 1045 (28000): Access denied for user ‘root’@'localhost’错误，
在网上搜了一下，得到如下解决方法：'

{% highlighting bash %}
# /etc/init.d/mysql stop
# mysqld_safe --user=mysql --skip-grant-tables --skip-networking &
# mysql -u root mysql
mysql> UPDATE user SET Password=PASSWORD('newpassword') where USER='root';
mysql> FLUSH PRIVILEGES;
mysql> quit

# /etc/init.d/mysqld restart
# mysql -uroot -p
Enter password:

mysql>
{% endhighlight %}

