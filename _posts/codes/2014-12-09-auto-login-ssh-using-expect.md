---
layout: article
title: "Auto Login SSH Using Expect"
modified:
categories: codes
excerpt:
tags: []
image:
  feature:
  teaser:
  thumb:
date: 2014-12-09T10:48:19+08:00
---

{% highlight bash %}
#!/usr/bin/expect -f
set timeout -1
set pwd 'yourpwd'
spawn ssh username@servername/ip
expect 'password:'
send '$pwd\r'
interact
{% endhighlight %}
