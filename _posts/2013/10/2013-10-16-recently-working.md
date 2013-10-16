---
layout: post
title: 最近的做的事儿
tags: [生活, 工作]
image:
  feature: abstract-8.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
comments: true
share: true  
---

给自己做个流水帐，记一下最近做的东西：

* 尝试微信公众平台开发

    这个是当时领导交代的一个任务，刚好我最近也在关注这个东西，就拿来做做，语言用的是最近正在学习的python，
    基于微信处理框架[WeRoBot](https://github.com/whtsky/WeRoBot)，部署在百度的BAE上，WeRoBot官方提供了SAE的示例，
    但BAE和SAE还是有少许不同的，做了相应的修改，果断时间把代码整理一下会开源出来的。

    其中涉及到中文分词的使用了[jieba](https://github.com/fxsjy/jieba)，同样因为BAE的特殊性，做了相应的修改，主要是jieba分词
    时要生成缓存文件，而BAE的缓存文件不再默认的路径。放弃SAE（因为WeRoBot，所以最开始是在SAE上做的）最主要原因也就是SAE的python不支持缓存文件，
    虽然提供有分词和缓存服务，但为了移植性只能放弃了。

    同时在github上找了个查询天气的python脚本，自己也做了修改和包装，之后也会一并放出代码，会专门写一篇博客介绍相关东西的。

* 重装系统

    本来这个不算事儿的，这里拿来说是因为在这个过程中开始尝试把一些常用的插件和操作自动化，现在才刚刚开始，做的还很糙，
    同样放在github上，见[qiulin/scripts](https://github.com/qiulin/scripts)。同时不得不说，在桌面linux方面，ubuntu真的可以甩其他发行版好几条大街。

* 研究glusterfs

    GlusterFS是一个比较有名的聚合式文件系统，这个也算是工作上的任务，现在还只是做一些简单的测试，同时中文文档比较少和比较老，
    需要自己去啃相关的英文文档，就当学英文了，有些文档会力所能及的翻译一下的。

* 学习《深入理解计算机操作系统》

    这个算是进度比较慢的，因为自己的计算机方面的基础比较薄弱，要好好充电，也欢迎大家监督。

---

跑一下题，说一下自己未来一段时间想做的事儿：

* 想研究一下开源硬件，Arduino或者Raspberry Pi吧，感觉应该会很Cool，嘎嘎！

* 学习Linux系统开发，算是对系统的进一步了解和实战吧。

-EOF-
