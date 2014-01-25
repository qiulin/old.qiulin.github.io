---
layout: post
title: "解决glusterfs的peer rejected问题"
tag: ["glusterfs"]
comments: true
share: true
---

今天早上检查gluster节点状态，发现其中gfs0和gfs1互相报对方节点状态为peer rejected，如下所示：

{% highlight bash %}
[root@gfs0 2013]# gluster peer status
Number of Peers: 2

Hostname: gfs1
Uuid: 39f51993-5c31-45d3-a879-5258d1b4733b
State: Peer Rejected (Connected)

Hostname: gfs2
Uuid: 09f8b75c-af4c-48fa-b936-442578246db1
State: Peer in Cluster (Connected)
{% endhighlight %}

查阅了gluster的官方文档，里面有解决方法：

1. Stop glusterd
2. In /var/lib/glusterd, delete everything except glusterd.info (the UUID file)
3. Start glusterd
4. Probe one of the good peers
5. Restart glusterd, check 'gluster peer status'
6. You may need to restart glusterd another time or two, keep checking peer status.

ref: [Resolving Peer Rejected](http://www.gluster.org/community/documentation/index.php/Resolving_Peer_Rejected)

但还是遇到比较奇葩的问题，就是gfs0和gfs1互报问题，但gfs2又报两个都是好的，这样就搞不清楚到底是gfs0还是gfs1出问题，
这样我就选择修复gfs1，但修复完之后再次检查状态又发现gfs2也报peer rejected了，然后又修复gfs2。然后，你没猜错，gfs2又报gfs0 rejected了。
只能又修复gfs0，这样子就修复了一圈，虽然最后问题解决了，但这样子总归不是个办法，留个问题继续研究吧，有头绪了再写。

-EOF-
