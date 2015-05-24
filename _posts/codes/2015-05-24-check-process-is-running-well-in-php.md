---
layout: article
title: "Check Process is Running Well in PHP"
modified:
categories: codes
excerpt:
tags: []
image:
  feature:
  teaser:
  thumb:
date: 2015-05-24T16:49:40+08:00
---

{% highlight php %}
function is_running_well($pid, $timeout) {
    // get etime
    exec("ps -eo pid,etime |grep $pid |awk '{print $2}'", $ret);

    // is running or not
    if (empty($ret)) {
        return false;
    }

    // no timeout limited
    if ($timeout == 0) {
        return true;
    }

    // is timeout or not

    // [[DD-]hh:]mm:ss
    $etime = $ret[0];
    $etime = array_reverse(explode('-', $etime));
    $time = current($etime);
    $days = (int)next($etime);

    $his = array_reverse(explode(':', $time));
    $seconds = (int)current($his);
    $minutes = (int)next($his);
    $hours = (int)next($his);

    $eseconds = $days * 86400 + $hours * 3600 + $minutes * 60 + $seconds;

    return $timeout > $eseconds ? true : false;
}
{% endhighlight %}
