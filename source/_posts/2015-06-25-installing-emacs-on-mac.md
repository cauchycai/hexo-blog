---
title: "Mac 上安装 Emacs 的几种选择"
date: 2015-06-25 00:00:00
tags: [emacs, osx, mac, software]
---


* brew 中的默认版本

{% codeblock bash %}
$ brew install --cocoa emacs
$ brew linkapps emacs
{% endcodeblock %}

* 一个日本网友提供的版本，也是brew安装，很不错，推荐此版本。

{% codeblock bash %}
$ brew tap railwaycat/emacsmacport
$ brew install emacs-mac
$ brew linkapps emacs-mac
{% endcodeblock %}

* "Emacs for Mac OS X" http://emacsformacosx.com , 号称很Pure。

* AquaEmacs：http://aquamacs.org
