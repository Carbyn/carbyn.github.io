---
layout: article
title: "A Simple Shell Script to Stat Svn Log"
modified:
categories: codes
excerpt:
tags: []
image:
  feature:
  teaser:
  thumb:
date: 2014-12-08T18:46:03+08:00
---

{% highlight bash %}
#!/bin/bash

user=`whoami`

workspace=~/svn_root_path

revs=./revs
paths=./paths

startdate=`date +%F`
enddate=`date +%F`

cleanUp() {
    rm -f $revs $paths
}

Usage() {
    echo "bash $0 -d 3";
    echo "bash $0 -r 2014-09-10 2014-09-19";
}

cleanUp

if [ $# -eq 0 ];then
    Usage;exit 1;
fi

while getopts ":d:r:" opt; do
    case "$opt" in
        d) startdate=`date -d "$2 day ago" +%F`
            ;;
        r) startdate=$2; enddate=$3
            ;;
        *) echo "param error"; Usage; exit 1
            ;;
    esac
done

svn log -r {$startdate}:{$enddate} $workspace|grep $user|awk '{print $1}' > $revs

touch $paths
while read rev
do
    svn log -vr $rev|grep "^ "|awk '{print $2}' >> $paths
done < $revs

echo $startdate:$enddate
cat $paths|sort|uniq

cleanUp
{% endhighlight %}
