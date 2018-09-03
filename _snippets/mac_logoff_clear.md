---
label: snippets
layout: post
title: Cleaning Browser Auth Cookies at Mac OS X log off
short_title: Mac Log Off Clearing Script
author:
  name: jd
tags:
- google
- tool
category: tutorial
lead: How to use a __logoff script__ to clear authenticated web sessions on a Mac
published: true
date: 2018-09-03
---
{% include lead.md %}

### Introduction

If you use a __shared__ or __public account__ on a Mac running Mac OS X, but are worried about forgetting to sign out of your web sessions, this might be the __script solution__ for you.

### Method

__Download__ and __install__ the latest __Offset.pkg__ file from this excellent [Github respository][1]{:target="_blank" rel="noopener"}.

__Create__ a logout script, such as logout.sh, by typing the following command on the terminal:

{% highlight shell %}
sudo nano /usr/local/offset/logout-every/logout.sh
{% endhighlight %}

__Paste__ in the following script, ammending it if you require __current__ or __all__ users to be cleared:

{% highlight shell %}
#!/bin/sh
set +e

rm -Rf /Users/$USER/Library/Keychains/*
rm -Rf /Users/$USER/Library/Google/
rm -Rf /Users/$USER/Library/Safari/*.plist
rm -Rf /Users/$USER/Library/Cookies/*
rm -Rf /Users/$USER/Library/Application Support/Google/Chrome/
rm -Rf /Users/$USER/Library/Caches/com.apple.Safari
rm -Rf /Users/$USER/Library/Caches/com.google.*
rm -Rf /Users/$USER/Library/Caches/Google/
rm -Rf /Users/$USER/Library/Preferences/com.google.*

rm -Rf /Users/*/Library/Keychains/*
rm -Rf /Users/*/Library/Google/
rm -Rf /Users/*/Library/Safari/*.plist
rm -Rf /Users/*/Library/Cookies/*
rm -Rf /Users/*/Library/Application Support/Google/Chrome/
rm -Rf /Users/*/Library/Caches/com.apple.Safari
rm -Rf /Users/*/Library/Caches/com.google.*
rm -Rf /Users/*/Library/Caches/Google/
rm -Rf /Users/*/Library/Preferences/com.google.*

exit 0
{% endhighlight %}

__Permission__ the new script properly:

{% highlight shell %}
sudo chown -R root:wheel /usr/local/offset/logout-every/logout.sh
sudo chmod -R 755 /usr/local/offset/logout-every/logout.sh
{% endhighlight %}

__Logout__, __reboot__ and then __log back in__ to test that the user has been signed out of all web sessions. You can also check the log to see if the script is running here:

{% highlight shell %}
cat /var/log/offset.log
{% endhighlight %}

  [1]: https://github.com/aysiu/offset/releases "Automatically process packages and scripts at logout"