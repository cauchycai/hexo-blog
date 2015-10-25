---
layout: post
title: "在svn库中使用git"
description: ""
category: setup
tags: [git]
---


初始化Git版本库；忽略svn版本库文件夹 => .svn；添加项目文件到git库。

{% highlight bash %}
$ cd svn_repo
$ git init
$ echo ".svn" > .gitignore
$ git add --all
$ git commit -m "first commit"
{% endhighlight %}

设置svn忽略git版本库相关的文件。

{% highlight bash %}
$ svn propset svn:ignore ".git*" .
$ svn commit -m "忽略git版本库文件"
{% endhighlight %}

之后就可以在svn库里使用git的branch功能了。

这样就可以一定程度上解决一个功能写了好久只写到一半却不敢提交的问题。具体可以这样使用：

1> 当我们做一个大功能时，新开一个branch; 切到这个branch进行开发：

{% highlight bash %}
$ git branch newui
$ git checkout newui
{% endhighlight %}

2> 写到一半来了个紧急需求，得赶紧上。。好吧。。先切回来把这个任务做掉：

{% highlight bash %}
$ git checkout master
{% endhighlight %}

3> 代码回到了之前的状态，先把小功能改完然后提交：

{% highlight bash %}
$ git commit -m "某个紧急问题"
$ svn commit -m "...."
{% endhighlight %}

4> ok,去测吧。继续做newui

{% highlight bash %}
$ git checkout newui
{% endhighlight %}

5> n久之后终于把newui做完可以提交svn了

{% highlight bash %}
$ git checkout master
$ git merge newui
$ svn commit -m "new ui"
{% endhighlight %}

