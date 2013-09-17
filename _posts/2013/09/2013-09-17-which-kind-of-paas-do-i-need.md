---
layout: post
title: 我需要怎么样的PAAS平台
tags: [PAAS]
image:
  feature: abstract-3.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
comments: true
share: true
---

最近领导提出来给公司的微信公众号加点小功能，就自己注册了公众号先玩一下，就当测试了。

选择语言Python，选择微信机器人框架WeRoBot，查阅了一些资料，下午开始干活，因为WeRoBot提供有一个SAE的demo，
所以就选择在SAE部署一下做开发测试，下午在公司进行的还算顺利，但晚上回去用自己的电脑继续干活噩梦就开始了。

先是SAE的svn死活签不出代码，一直提示如下错误

{% highlight bash %}
svn: OPTIONS of 'https://svn.sinaapp.com/geekping': could not connect to server (https://svn.sinaapp.com)
{% endhighlight %}

Google和官方论坛寻找都无果，所以就在微博上抱怨了一下，朋友推荐用BAE，结果试用了一下，选择git部署代码，git也是各种抽风，
一直到写这篇东西的时候，我还是没有push上去点有用的代码。期间重建了三次应用，重新签出无数次。也是各种查资料和文档无果。

**可能是我今天打开的方式不对吧**

经过这各种虐，我想说说**什么是我想要的PAAS平台**，针对国内的PAAS平台。

* 尽可能的和原生环境相同

    现在的PAAS环境多少和原生环境还是有点差异的，有些是为了添加自己的服务，也有些是基于安全考虑禁用掉了一些功能。
    虽然看似很小的修改，如果从头写的话，可能不会有太大的影响，但如果是把已有的系统迁移过去简直就是灾难，如果再碰到原来的代码
    不是自己写的，那肯定死的心都有了。

* 稳定
    
    虽然，各家都声称自家的PAAS平台经过了自家多少应用和流量的检验，是的，我也相信，但各种周边系统的稳定性实在不敢恭维。
    SAE的论坛上大家抱怨svn不稳定不是一天两天了，但貌似也没有太大的改观。

* 文档
    
    前面也说了，各种PAAS平台和原生系统多少有点差别，所以说清楚这种差别就至关重要了。但我看了SAE和BAE上面的很多文档和实例，
    大多数就是一句话啊。*文档!文档！文档！！！*

写了这些，心情也慢慢平复了，但今天写代码的心情是完全没有了，应该还是因为我比较菜吧，或许是因为打开的方式不对。

-EOF-
