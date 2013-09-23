---
layout: post
title: GlusterFS网络配置技巧
modified: 2013-09-15
tags: [运维, GlusterFS]
image:
  feature: abstract-8.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
comments: true
share: true  
---

最近在研究GlusterFS，中文的文档比较少，自己翻译一下，这一篇是[Network Configuration Techniques](http://www.gluster.org/community/documentation/index.php/Network_Bonding)）

##绑定最佳实践

网络接口绑定（聚合）把不同的物理接口合并成一个逻辑接口，只有一个IP地址。
一个N路聚合接口能够减少N-1个物理接口，在某些情况下性能能够得到改善。

###什么时候需要绑定

* 网络连接需要HA
* 工作负载：连续访问大文件（大多数时间消耗在读写上）
* Client/Server吞吐量限制 << （远小于）存储吞吐量限制
    * 1 GbE（大多数情况）
    * 10-Gbps连接或更快——对于写操作来说，复制加倍了网络负载，而且，复件通常保存在
    不同的节点上，Client可以在节点直接并行传输。
* **限制**：如果网络节点不在同一个VLAN上，网络聚合并不会改善吞吐量。

###如何配置

* [如何绑定](http://www.linuxquestions.org/linux/answers/Networking/Linux_bonding_howto_0)
* Gluster Client最佳绑定模式是mode6（balance-alb），该模式允许分离网络接口卡的client大部分时间能够并行传输写操作。
我们考察一个单独Client的write吞吐量峰值为750MB/s，做了2个10-GbE端口的mode6的特大帧（jumbo frames）端口聚合，
它的网络流量为1.5GB/s。（这句翻译不好，原文为：A peak throughput of 750MB/s on writes from a single client was observed
with bonding mode 6 on 2 10-GbE NICs with jumbo frames. That's 1.5GB/s of network traffic.）

##特大帧Jumbo frames

特大帧（Jumbo Frames）是长度大于1500bytes的以太网（或无限带宽技术）帧（无限宽带技术帧默认是2000bytes左右）。
增加帧的大小可以降低操作系统和硬件的负载，操作系统和硬件必须处理每一帧的中断和协议信息。

###什么时候需要配置

* 所有比1-GbE快的网络
* 负载为连续大文件读写
* **限制**：要求VLAN中的所有网络交换机都必须配置成处理特大帧，否则不要配置特大帧。

###怎么配置

* 编辑网络接口文件/etc/sysconfig/network-scripts/ifcfg-your-interface
* 以太网Ethernet（ixgbe驱动）：给网络接口文件添加“MTU=9000”（MTU表示“最大传输单位”）记录
* 无限带宽技术（mlx4驱动）：给网络接口配置文件添加“CONNECTED_MODE=yes”和“MTU=65520”记录
* ifdown your-interface; ifup your-interface
* 测试“ping -s 16384 同个VLAN的其他主机”
* 因为协议头，把要求的最大帧大小换成比MTU大，通常为9216bytes

##配置存储的后端网络

该方法能让你通过把流量分配到不同协议的不同网络接口上来增加不同协议站点的网络容量。该方法能降低延迟、改善网络吞吐量。
例如，该方法能够保持系统自愈和通过和同一个网络端口的非Gluster客户端竞争来重新均衡负载，并且能够更好的支持多数据流IO。
（这一句翻不好，原文为：For example, this method can keep self-heal and rebalancing traffic from competing with non-Gluster
client traffic for a network interface, and will better support multi-stream I/O.）

###什么时候需要配置

* Gluster服务端提供非Gluster服务时，比如NFS, Swift(REST), CIFS等。对Gluster客户端没有什么帮助（额外的Gluster挂载节点）。
* 网络端口是over-utilized。

###怎么配置

* 大多数网卡是有多端口的，把端口1分配给非Gluster服务端口，端口2分配给Gluster服务端口。
* 为简化配置，把Gluster服务端口和非Gluster服务端口分配到不同的VLAN网段。

*ps.*

第一次翻技术文档，翻译的不是很好，语言也不太通顺，欢迎大家提建议。

-EOF-
