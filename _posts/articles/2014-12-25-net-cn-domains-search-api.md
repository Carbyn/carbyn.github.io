---
layout: article
title: "Net.cn Domains Search API"
modified:
categories: articles
excerpt:
tags: []
image:
  feature:
  teaser:
  thumb:
date: 2014-12-25T16:44:41+08:00
---

<p>
  <strong>The API uses HTTP protocol, both GET and POST are supported.</strong>
  <br>url: http://panda.www.net.cn/cgi-bin/check.cgi
  <br>params: area_domain
  <br>example: http://panda.www.net.cn/cgi-bin/check.cgi?area_domain=carbyn.cc
</p>

<p>
  <strong>The result is in xml format:</strong>
  {% highlight xml %}
  <?xml version="1.0" encoding="gb2312"?>
  <property>
  <returncode>200</returncode>
  <key>carbyn.cc</key>
  <original>211 : In Use</original>
  </property>
  {% endhighlight %}
</p>

<p>
  <strong>xml description</strong>
  <br>returncode: 200 means return success
  <br>key: the domain searched
  <br>original:
    <br>210: Domain name is available
    <br>211: Domain name is not available
    <br>212: Domain name is invalid
    <br>213: Time out
</p>
