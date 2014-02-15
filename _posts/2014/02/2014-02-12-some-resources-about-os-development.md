---
layout: post
title: "关于操作系统开发的一些资料"
tag: ["开发", "操作系统"]
comments: true
share: true
---

最近一直在看操作系统的知识，但纯理论的东西只看看理解不了，也记不住，
刚好看到一个自己实现操作系统（只是一个kernel）的项目[MikeOS](http://mikeos.berlios.de/)，
所以就萌生了实践一下的念头，但该项目完全是汇编代码实现的，目前还玩不了，
在它的相关资料里找到了一些C实现的例子，所以就打算照猫画虎吧，在github上也创建了一个repo，用来托管代码，并起了一个很二的名字，
[HuskyOS](https://github.com/qiulin/HuskyOS)，哈士奇，之前我家里养过一只，著名的井犬。

下面是搜集到的一些资料：

* [JamesM's kernel development tutorials](http://www.jamesmolloy.co.uk/tutorial_html/index.html).This set of tutorials aims to take you
 through programming a simple UNIX-clone operating system for the x86 architecture.The tutorial uses C as the language of choice,
 with liberally mixed in bits of assembler.

* [MikeOS](http://mikeos.berlios.de).MikeOS is an operating system for x86 PCs, written in assembly language.

* [Bran's kernel development tutorials](http://www.osdever.net/bkerndev/index.php).

* [Osdever.net's wiki](http://wiki.osdev.org/Main_Page).

* [Xv6, a simple Unix-like teaching operating system](http://pdos.csail.mit.edu/6.828/2012/xv6.html).

* [Practical File System Design:The Be File System](http://www.nobius.org/~dbg/practical-file-system-design.pdf).

* [Linux汇编语言开发指南](https://www.ibm.com/developerworks/cn/linux/l-assembly/), a tutorial about Linux assembly development.

* [EmilOS](https://github.com/kiljacken/EmilOS). EmilOS is a hobby operating system, based on the code from JamesM's kernel develpment 
 tutorial series.

* [hurlex](https://github.com/hurlex25/hurlex). 一个运行在x86-IA32架构下的小内核，仅作为操作系统理论学习的参考。
