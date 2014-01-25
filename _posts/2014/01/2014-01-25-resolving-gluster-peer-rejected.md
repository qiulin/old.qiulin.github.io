---
layout: post
title: "���glusterfs��peer rejected����"
tag: ["glusterfs"]
comments: true
share: true
---

�������ϼ��gluster�ڵ�״̬����������gfs0��gfs1���౨�Է��ڵ�״̬Ϊpeer rejected��������ʾ��

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

������gluster�Ĺٷ��ĵ��������н��������

1. Stop glusterd
2. In /var/lib/glusterd, delete everything except glusterd.info (the UUID file)
3. Start glusterd
4. Probe one of the good peers
5. Restart glusterd, check 'gluster peer status'
6. You may need to restart glusterd another time or two, keep checking peer status.

ref: [Resolving Peer Rejected](http://www.gluster.org/community/documentation/index.php/Resolving_Peer_Rejected)

�����������Ƚ���������⣬����gfs0��gfs1�������⣬��gfs2�ֱ��������Ǻõģ������͸㲻���������gfs0����gfs1�����⣬
�����Ҿ�ѡ���޸�gfs1�����޸���֮���ٴμ��״̬�ַ���gfs2Ҳ��peer rejected�ˣ�Ȼ�����޸�gfs2��Ȼ����û�´�gfs2�ֱ�gfs0 rejected�ˡ�
ֻ�����޸�gfs0�������Ӿ��޸���һȦ����Ȼ����������ˣ����������ܹ鲻�Ǹ��취��������������о��ɣ���ͷ������д��

-EOF-
