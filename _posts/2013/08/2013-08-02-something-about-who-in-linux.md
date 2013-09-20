---
layout: post
title: 由linux的who引发的一些事情
modified: 2013-09-21
tags: [Linux]
image:
  feature: abstract-4.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
comments: true
share: true
---

今天进行服务器例行检查，执行了who之后发现居然有两个用户在登陆，其中一个已经很多天没有活动了，因为有之前被黑的阴影，所以就一直追着这个东西检查。

ps看了一下也没有什么异常进程，不过后来发现有一个vncserver进程跑着，突然想起之前安装某个东西的时候把vnc启起来了，推测可能和这个有关，后来把vncserver kill掉之后，重新who了一下，发现正常了。

之前启动vnc的时候也把inittab修改成5了，因为只需要用那么一次，重新修改成3。暂时还不清楚有没有其他的副作用，比如vncserver的配置什么的，先记录下来以观后效吧。

总结的一点经验教训，以后服务器安装完东西之后，还是要做好善后工作的，把一些没必要保留的文件、配置和服务什么的还是要尽快停掉。

**ps.**

最近在研究nginx，只要是一些内部的原理什么的，另外涉及到一些模块开发的东西，虽然做了运维，但还是有那么点开发的情节，就算在这里挖个坑吧，以后慢慢填。
