---
layout: post
title: "在fedora19上安装mysql"
tags: [mysql, fedora]
comments: true
share: true
---

fedora19安装mysql（新的名字叫mariadb，因为sun被oracle收购，原mysql作者发起的兼容mysql的数据库）

{% highlight bash %}
yum install mysql-server mysql -y
{% endhighlight %}

在fedora 19上第一次使用mysql，一下子不知道怎么启动mysql服务，试了service和/etc/init.d都不行，查了下资料，可以按照下面步骤操作：

{% highlight bash %}
systemctl start msyqld.service
systemctl enable mysqld.service  
#根据字面意思是启用msyqld服务，下面就可以用service来管理mysqld了
service mysqld status
...
service msyqld stop

# 登陆mysql
mysql -u root -p
{% endhighlight %}

**ps.**

具体systemctl是怎么管理服务的，以后有时间在研究，先挖个坑...

-EOF-
