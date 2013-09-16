---
layout: post
title: 利用inotify和rsync实现实时备份
modified: 2013-09-15
tags: [运维, 备份]
image:
  feature: abstract-10.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
comments: true
share: true  
---

之前接手的一台服务器上的一些重要文件没有备份（虽然可以重新生成，但文件数量比较大，重新生成代价很大），
因为这些文件是会经常产生新的文件的，所以考虑采用inotify+rsync来做实时备份。下面是做的一些记录。

inotify是linux内核提供的一种通知机制，当监听的文件动作发生时，就可以触发相应的动作，
这里是用来触发rsync来做备份。inotify-tools是基于inotify实现的终端工具，
也是我们这里真正要用到的。rsync的remote sync的简称，自然是来做远程备份的。


inotify+rsync的配置文档网上很多，下面分享一个经过测试可用的。
[http://dl528888.blog.51cto.com/2382721/771533]

基本上照着做就可以了，但我用的还稍有不同，
为了防止误删操作，所以我这里对“删除”操作时不进行监听的，
主要体现在同步脚本里。

{% highlight bash %}
host=192.168.10.221  
src=/tmp/         
des=web 
user=webuser 
/usr/local/inotify/bin/inotifywait -mrq --timefmt '%d/%m/%y %H:%M' --format '%T %w%f%e' -e     modify,delete,create,attrib $src \  #这里取消delete监听
| while read files  
do  
/usr/bin/rsync -vzrtopg --delete --progress --password-file=/usr/local/rsync/rsync.passwd $src $user@$host::$des  #不要--delete选项
echo "${files} was rsynced" >>/tmp/rsync.log 2>&1  
done
{% endhighlight%}

-EOF-
