---
layout: post
title: Python嵌套try/except异常
tags: [Python]
image:
  feature: abstract-9.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
comments: true
share: true  
---

直接上代码，了解的人能看懂的。

{% highlight python %}
#!/usr/bin/env python
s1 = {2}
s2 = {}

try:
    i1 = s1.pop()
    print "T1"
    try:
        i2 = s2.pop()
        print "T2"
    except:
        print "E2"
except:
    print "E1"
{% endhighlight %}

-EOF-
