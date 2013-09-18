---
layout: post
title: 给hpstr-jekyll-theme提交了一个pull request
tags: [code, jekyll]
image:
  feature: abstract-6.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
comments: true
share: true
---

昨天晚上给hpstr-jekyll-theme（也就是我当前使用的主题）提交了一个pull request，解决的问题很简单，
就是在post页面中，下一篇博文的read more内容显示的还是当前博文的内容，
看了一下*_layout/post.html*的源码，引起问题的源码如下：

<script src="https://gist.github.com/qiulin/f8fcb4e67887f30954a0.js"></script>

*content*表示的是当前文章的内容，要fixbug只要改为*post.content*就可以了。

今天早上看到作者已经接受了这个pull request，也已经合并到master分支里面了。
虽然是一件很小的事儿，但带来的成就感，绝对比DotA强多了。也秀了一下自己惨不忍睹的英语。

再次推荐这个jekyll主题，**高大上**，地址github自己找。

*ps.*

因为源码中含有jekyll标签，所以用gist来贴代码

-EOF-
