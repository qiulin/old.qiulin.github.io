---
layout: post
title: 解决glusterfsd无法启动的问题
modified: 2014-02-25
tags: ["glusterfs"]
image:
  feature: abstract-6.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
comments: true
share: true
---

这两天又在鼓捣glusterfs，在检查volume状态的时候遇到一个问题，gfs0节点的NFS Server和Self-heal Daemon的状态显示offline，
重启了glusterd也没有效果，经过半个下午的奋战问题终于解决了，下面记录一下解决问题的详细过程。

1. 通过<code>gluster volume status</code>命令可以查看到其他节点对应服务的pid。

2. 由pid可以看到其他节点中，该服务的详细运行参数。

3. 由服务详细的运行参数可以看到服务的日志。

4. 查日志发现错误的详细信息：
    
    O-socket.glusterfsd: binding to failed: Address already in use.

5. 由日志知道，错误是由地址和端口占用引起的，但netstat -nltp看到了一下，对应端口并没有使用，同时gluster volume status显示的
故障节点该服务的pid并不存在，这就有点晕了。

6. 后来注意到该服务详细运行参数中有该服务的pid file文件和socket file文件，一下子顿悟了，原来是之前某个事件点的pid文件和socket文件
没有删除，才引起地址和端口占用问题。删除这些文件后，重启服务，一切OK。

虽然现在说起来挺轻松的，但这个问题确实浪费了我半个下午，可能还是自己太菜吧，继续好好学习。


-EOF-
