---
layout: article
title: "Configure Bridge Network on CentOS inside VMWare"
modified:
categories: articles
excerpt:
tags: []
image:
  feature:
  teaser:
  thumb:
date: 2015-06-06T20:28:41+08:00
---

<p>First, select bridged(autodetect) in network adapter settings.</p>
<p>Second, configure network on CentOS.<p>
{% highlight bash %}
# /etc/sysconfig/network
NETWORKING=yes
GATEWAY=192.168.1.1 

# /etc/sysconfig/network-scripts/ifcfg-eth0, which is the default network device
DEVICE=eth0
BOOTPROTO=static
IPADDR=192.168.1.100
BROADCAST=192.168.1.255
NETMASK=255.255.255.0
GATEWAY=192.168.1.1
ONBOOT=yes
TYPE=Ethernet
DNS1=8.8.8.8
{% endhighlight %}
