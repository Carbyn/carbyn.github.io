---
layout: article
title: "IP 2 Location in China"
modified:
categories: codes
excerpt:
tags: []
image:
  feature:
  teaser:
  thumb:
date: 2016-01-10T18:33:03+08:00
---

{% highlight php %}
<?php
if ($argc == 1 || !$argv[1]) die("ip not passed\n");
$url = 'https://sp0.baidu.com/8aQDcjqpAAV3otqbppnN2DJv/api.php?resource_id=6006&oe=utf8&query=%s';
$json = file_get_contents(sprintf($url, $argv[1]));
$data = @json_decode($json, true);
if (is_array($data) && $data['status'] == 0 && count($data['data']) > 0) {
    echo $data['data'][0]['location']."\n";
} else {
    echo 'unknown'."\n";
}
{% endhighlight %}
