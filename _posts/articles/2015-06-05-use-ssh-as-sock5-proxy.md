---
layout: article
title: "Use SSH as SOCK5 Proxy"
modified:
categories: articles
excerpt:
tags: []
image:
  feature:
  teaser:
  thumb:
date: 2015-06-05T14:28:41+08:00
---

{% highlight bash %}
ssh -N -f -i .ssh/yourprivate.pem user@server -D ip:port
{% endhighlight %}
