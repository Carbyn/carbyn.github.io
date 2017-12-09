---
layout: article
title: "Git Config"
modified:
categories: articles
excerpt:
tags: []
image:
  feature:
  teaser:
  thumb:
date: 2017-12-09T14:18:41+08:00
---

This is my ~/.gitconfig
{% highlight bash %}
[user]
	name = carbyn
	email = carbyn.wu@gmail.com
[credential]
	helper = store
[alias]
	st = status
	ci = commit --verbose
	co = checkout
	br = branch
[push]
	default = simple
{% endhighlight %}
