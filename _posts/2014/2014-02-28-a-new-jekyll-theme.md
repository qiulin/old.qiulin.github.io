---
layout: post
title: 换了一个新的jekyll主题Scribble
---

[Scribble](https://github.com/muan/scribble)是由**muan**创建的jekyll主题，在[chloerei](http://www.chloerei.com)那里看到的，非常简洁大方，挺适合单纯码字的，而且没有分类和标签支持，也省了每次都写那么大一坨头部（相对于hpstr而言），
也更有码字的动力了，缺少分类和标签支持也带来一个查找的问题，这主要通过搜索来弥补吧，准备给加个google的
自定义搜索。

之前使用的[HPSTR Jekyll Theme](https://github.com/mmistakes/hpstr-jekyll-theme)非常美观，但不太适合中文排版。


update:

对Scribble做了一些自己的定制，主要包括下面几个：

1. 添加了Google Custom Search Engine，只要在配置文件_config.yml里面添加自己的gcse id就好了。
2. 去除了原作者的Scribble图片。
3. 站点标题采用h1标签。
4. 去除了signoff，而用简单-eof-代替，同时增加了username参数。
5. 改善中文排版，因为typo.css的侵入问题，选择[entry.css](http://nodejs.in/Entry.css/)来做中文排版，但也做了自己的裁剪，主要集中在*代码高亮*，移除了entry.css的代码高亮（只保留了字体）。Entry.css官方提供的css文件没有进行代码格式化，看起来实在费眼。


下一步的计划：

1. ~~改善中文排版，考虑使用typo.css~~

考虑在合适的时候，把自己修改的版本作为一个单独的主题发布出来。
