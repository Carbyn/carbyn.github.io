---
layout: article
title: "Samba Add and Connect"
modified:
categories: articles
excerpt:
tags: []
image:
  feature:
  teaser:
  thumb:
date: 2015-05-25T12:28:41+08:00
---

{% highlight bash %}
### Add a new user
# First, a samba user must be a linux user. If it already exists, skip this step.
useradd -m username
passwd username

# Then, add a new samba user.
$SAMBA_HOME/bin/smbpasswd -a username

### Restart samba service
# Note that you do not need to do this after a new user is added.
pkill nmbd && pkill smbd
$SAMBA_HOME/sbin/nmbd -d && $SAMBA_HOME/sbin/smbd -D -s /etc/samba/smb.conf

### Connect to samba on Windows
# Open cmd, here we use 'net use' command to create a connection.
net use z: \\servername\username /savecred /persistent:yes

# Disconnect.
net use * /del
{% endhighlight %}
