---
layout: post
title: Django book阅读笔记1
tags: [Django]
image:
  feature: abstract-5.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
comments: true
share: true  
---

# 在Python代码中使用Django模板的最基本方式如下：

1。 可以用原始的模板代码字符串创建一个 Template 对象， Django同样支持用指定模板文件路径的方式来创建 Template 对象;

2. 调用模板对象的render方法，并且传入一套变量context。它将返回一个基于模板的展现字符串，模板中的变量和标签会被context值替换。

# 你可以根据需要使用任意多的继承次数。 使用继承的一种常见方式是下面的三层法：

1. 创建 base.html 模板，在其中定义站点的主要外观感受。 这些都是不常修改甚至从不修改的部分。

2. 为网站的每个区域创建 base_SECTION.html 模板(例如, base_photos.html 和 base_forum.html )。这些模板对 base.html 进行拓展，并包含区域特定的风格与设计。

3. 为每种类型的页面创建独立的模板，例如论坛页面或者图片库。 这些模板拓展相应的区域模板。这个方法可最大限度地重用代码，并使得向公共区域（如区域级的导航）添加内容成为一件轻松的工作。


# 以下是使用模板继承的一些诀窍：

1. 如果在模板中使用 <code>{% extends %}</code> ，必须保证其为模板中的第一个模板标记。 否则，模板继承将不起作用。

2. 一般来说，基础模板中的 <code>{% block %}</code> 标签越多越好。 记住，子模板不必定义父模板中所有的代码块，因此你可以用合理的缺省值对一些代码块进行填充，然后只对子模板所需的代码块进行（重）定义。 俗话说，钩子越多越好。

3. 如果发觉自己在多个模板之间拷贝代码，你应该考虑将该代码段放置到父模板的某个 <code>{% block %}</code> 中。

4. 如果你需要访问父模板中的块的内容，使用 <code>{{ block.super }}</code>这个标签吧，这一个魔法变量将会表现出父模板中的内容。 如果只想在上级代码块基础上添加内容，而不是全部重载，该变量就显得非常有用了。

5. 不允许在同一个模板中定义多个同名的 <code>{% block %}</code> 。 存在这样的限制是因为block 标签的工作方式是双向的。 也就是说，block 标签不仅挖了一个要填的坑，也定义了在父模板中这个坑所填充的内容。如果模板中出现了两个相同名称的 {% block %} 标签，父模板将无从得知要使用哪个块的内容。

6. <code>{% extends %}</code> 对所传入模板名称使用的加载方法和 get_template() 相同。 也就是说，会将模板名称被添加到 TEMPLATE_DIRS 设置之后。

7. 多数情况下， <code>{% extends %}</code> 的参数应该是字符串，但是如果直到运行时方能确定父模板名，这个参数也可以是个变量。 这使得你能够实现一些很酷的动态功能。
