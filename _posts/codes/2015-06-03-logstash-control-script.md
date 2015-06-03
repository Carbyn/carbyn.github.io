---
layout: article
title: "Logstash Control Script"
modified:
categories: codes
excerpt:
tags: []
image:
  feature:
  teaser:
  thumb:
date: 2015-06-03T15:46:03+08:00
---

{% highlight bash %}
#!/bin/bash
# logstash control script

export JAVA_HOME=/home/work/lib/java6
export PATH=${JAVA_HOME}/bin:${PATH}
export CLASSPATH=.:${JAVA_HOME}/lib/dt.jar:${JAVA_HOME}/lib/tools.jar

REALTIME=$(cd .. && pwd)
LOGSTASH_HOME=$REALTIME/logstash-1.4.1

################# functions ###################

function usage() {
    cat <<-usage
    Usage: $0 [start|stop|status|restart] logstash-conf-name
    The logstash-conf-name should located in conf dir, and without '.conf' suffix.
usage
}

function start() {
    echo "starting..."
    if [ ! -d $LOGSTASH_HOME/supervise/${1} ] ; then
        mkdir -p $LOGSTASH_HOME/supervise/${1}
    fi
    cd $LOGSTASH_HOME/supervise/${1} && rm lock status svcontrol
    $LOGSTASH_HOME/bin/supervise.logstash $LOGSTASH_HOME/supervise/${1} nohup $LOGSTASH_HOME/bin/logstash -f $LOGSTASH_HOME/conf/${1}.conf >> $LOGSTASH_HOME/logs/${1}.log 2>> $LOGSTASH_HOME/logs/${1}.err &
    echo "started"
}

function stop() {
    echo "stopping..."
    ps -ef |grep $LOGSTASH_HOME/bin/supervise.logstash |grep $LOGSTASH_HOME/conf/${1}.conf |grep -v grep |awk '{print $2}' |xargs kill -9
    ps -ef |grep $LOGSTASH_HOME/conf/${1}.conf |grep -v grep |awk '{print $2}' |xargs kill -9
    echo "stopped"
}

function status() {
    pid=`ps -ef |grep $LOGSTASH_HOME/conf/${1}.conf |grep -v grep |awk '{print $2}'`
    if [ "$pid" = "" ] ; then
        echo "not running"
    else 
        echo "running"
    fi
}

function restart() {
    stop $1
    start $1
}

################# functions ###################

#################### main #####################

if [ $# -ne 2 ] ; then
    usage
    exit 1
fi

if [ ! -f $LOGSTASH_HOME/conf/${2}.conf ] ; then
    usage
    exit 1
fi

case "x$1" in
    "xstart")
        start $2
        exit 0
        ;;
    "xstop")
        stop $2
        exit 0
        ;;
    "xstatus")
        status $2
        exit 0
        ;;
    "xrestart")
        restart $2
        exit 0
        ;;
    "*")
        usage
        exit 1
esac

#################### main #####################

{% endhighlight %}
