---
layout: post
title: 解决几个搭建gluster集群中遇到的问题
modified: 2014-02-17
tags: ["glusterfs"]
image:
  feature: abstract-3.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
comments: true
share: true
---

在搭建glusterfs集群的过程中（搭建过程参考[基于开源软件构建高性能集群NAS系统](http://blog.csdn.net/liuaigui/article/details/7163482)），
遇到了几个问题，所幸经过google都解决了，现记录如下：

* 按照文档搭建完之后，ctdb无法启动，报如下错误：
    
    Failed to connect client socket to daemon.

    Google发现public_addresses和nodes里面的地址配反了，gluster官方的HOWTO里有一个[CTDB HOWTO](http://www.gluster.org/community/documentation/index.php/CTDB)里面详细的配置。

    {% highlight bash %}
    /etc/dtdb/public_addresses:
        
    * List the VIPs that CTDB shoud create, you need one VIP for every Gluster server.
    
    /etc/ctdb/nodes
        
    * List the IPs on each physical interface.
    {% endhighlight %}

    简单说就是，public_addresses里面配的是虚拟VIP，即对外提供服务的IP，nodes里面配的是真实IP。

* Samba服务无法启动，继续Google发现是selinux的问题，需要关闭selinux。

    在不停机的情况下，关闭selinux的命令为：

    {% highlight bash %}
    # setenforce 0
    {% endhighlight %}
    永久关闭selinux的方法为：

    {% highlight bash %}
    # vi /etc/selinux/config

    ...

    SELINUX=disabled #由enforcing改为diabled
    {% endhighlight %}
-EOF-
