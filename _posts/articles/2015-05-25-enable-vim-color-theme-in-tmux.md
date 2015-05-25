---
layout: article
title: "Enable Vim Color Theme in Tmux"
modified:
categories: articles
excerpt:
tags: []
image:
  feature:
  teaser:
  thumb:
date: 2015-05-25T21:28:41+08:00
---

Setup ~/.tmux.conf, you can set the default-terminal to whatever you want
{% highlight bash %}
set -g default-terminal screen-256color
{% endhighlight %}

Start tmux like this, of course you can add an alias to your ~/.bashrc file
{% highlight bash %}
tmux -2
{% endhighlight %}
