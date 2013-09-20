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

这一段代码，但查不到intptr_t具体是什么东西，遂谷歌之。找到了这么一篇博客（[http://blog.csdn.net/justlinux2010/article/details/7490420](http://blog.csdn.net/justlinux2010/article/details/7490420)）intptr_t 其实不是指针类型，主要内容摘录如下：

    于是在linux的头文件中查找这个类型的定义，在/usr/include/stdint.h这个头文件中找到了这个类型的定义

{% highlight c %}
117 /* Types for 'void *' pointers.  */  
118 #if __WORDSIZE == 64  
119 # ifndef __intptr_t_defined  
120 typedef long int        intptr_t;  
121 #  define __intptr_t_defined  
122 # endif  
123 typedef unsigned long int   uintptr_t;  
124 #else  
125 # ifndef __intptr_t_defined  
126 typedef int         intptr_t;  
127 #  define __intptr_t_defined  
128 # endif  
129 typedef unsigned int        uintptr_t;  
130 #endif
{% endhighlight %}

    在《深入分析Linux内核源码》中找到了答案，原文描述如下：



**尽管在混合不同数据类型时你必须小心, 有时有很好的理由这样做. 一种情况是因为内存存取, 与内核相关时是特殊的. 
概念上, 尽管地址是指针, 内存管理常常使用一个无符号的整数类型更好地完成; 
内核对待物理内存如同一个大数组, 并且内存地址只是一个数组索引. 进一步地, 一个指针容易解引用; 
当直接处理内存存取时, 你几乎从不想以这种方式解引用. 使用一个整数类型避免了这种解引用, 因此避免了 bug. 
因此, 内核中通常的内存地址常常是 unsigned long, 利用了指针和长整型一直是相同大小的这个事实, 
至少在 Linux 目前支持的所有平台上.**

**因为其所值的原因, C99 标准定义了 intptr_t 和 uintptr_t 类型给一个可以持有一个指针值的整型变量. 
但是, 这些类型几乎没在 2.6 内核中使用**

文档参见http://oss.org.cn/kernel-book/ldd3/ch11.html

另外找到一篇关于c位运算很有用的文章http://blog.chinaunix.net/uid-20488859-id-1941166.html
