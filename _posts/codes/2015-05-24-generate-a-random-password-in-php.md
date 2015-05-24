---
layout: article
title: "Generate-a-Random-Password-in-PHP"
modified:
categories: codes
excerpt:
tags: []
image:
  feature:
  teaser:
  thumb:
date: 2015-05-24T20:46:03+08:00
---

{% highlight php startinline %}
$chars = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!@#$%^&*()';
for($i = 0; $i < 10; $i++) {
    $str .= substr($chars, rand(0, 1000) % strlen($chars), 1);
}
echo $str."\n";
{% endhighlight %}
