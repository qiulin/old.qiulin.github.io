---
layout: post
title: Nginx源码中的intptr_t
modified: 2013-09-21
tags: [Nginx, code]
image:
  feature: abstract-3.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
comments: true
share: true
---

最近在读nginx的源码，在/src/core/ngx_config.h中有

{% highlight c %}
typedef intptr_t ngx_int_t;
typedef uintptr_t ngx_uint_t;
{% endhighlight %}

这一段代码，但查不到intptr_t具体是什么东西，遂谷歌之。找到了这么一篇博客intptr_t 其实不是指针类型，主要内容摘录如下：


