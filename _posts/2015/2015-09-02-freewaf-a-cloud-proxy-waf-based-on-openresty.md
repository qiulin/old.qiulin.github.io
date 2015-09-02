---
title: "FreeWAF, 一个基于 Nginx + Lua 的 WAF"
tags: ["FreeWAF", "Nginx", "Lua"]
layout: post
---

最近在关注基于 Nginx + Lua ( OpenResty ) 的 WAF 解决方案，国内的 @loveshell 开源开源了一个 [ngx_lua_waf](https://github.com/loveshell/ngx_lua_waf)，了解了一下基本功能还是有的，但规则比较简单，总体来说不太满足需求。后来又找了半天，终于又找到了一个国外开源的 FreeWAF，基于和 ModSecurity 相似的规则集，当然写法不太一样，是作者基于自己的硕士论文实现的，有理论又有实践。



FreeWAF 的规则集是基于 Lua 的 table 构建的，读写都比较麻烦，作者说他会找一个更好的方式，但我没有找到，所以就自己撸袖子开干吧。



选择的方式是使用 yaml 来定义规则，然后通过一个 python 脚本，通过 yaml 的配置构建 lua table 文件结构，在这个过程中主要使用了 PyYAML 和 jinja2 这两个工具。



现在只完成了一个 demo，证明这样子基本可行，最近挤时间完善一下，同时，把作者的论文好好读一下。

-eof-