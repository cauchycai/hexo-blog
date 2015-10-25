---
layout: post
title: "Mac 上安装 Emacs 的几种选择"
description: ""
tags: [emacs, osx, mac, software]
---


* brew 中的默认版本

{% highlight bash %}
$ brew install --cocoa emacs
$ brew linkapps emacs
{% endhighlight %}

* 一个日本网友提供的版本，也是brew安装，很不错，推荐此版本。

{% highlight bash %}
$ brew tap railwaycat/emacsmacport
$ brew install emacs-mac
$ brew linkapps emacs-mac
{% endhighlight %}

* "Emacs for Mac OS X" http://emacsformacosx.com , 号称很Pure。

* AquaEmacs：http://aquamacs.org
