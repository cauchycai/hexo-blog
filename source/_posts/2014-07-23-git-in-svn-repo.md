---
title: "在svn库中使用git"
date: 2014-07-23 00:00:00
tags: [git]
---


初始化Git版本库；忽略svn版本库文件夹 => .svn；添加项目文件到git库。

{% codeblock lang:bash %}
$ cd svn_repo
$ git init
$ echo ".svn" > .gitignore
$ git add --all
$ git commit -m "first commit"
{% endcodeblock %}

设置svn忽略git版本库相关的文件。

{% codeblock lang:bash %}
$ svn propset svn:ignore ".git*" .
$ svn commit -m "忽略git版本库文件"
{% endcodeblock %}

之后就可以在svn库里使用git的branch功能了。

这样就可以一定程度上解决一个功能写了好久只写到一半却不敢提交的问题。具体可以这样使用：

1> 当我们做一个大功能时，新开一个branch; 切到这个branch进行开发：

{% codeblock lang:bash %}
$ git branch newui
$ git checkout newui
{% endcodeblock %}

2> 写到一半来了个紧急需求，得赶紧上。。好吧。。先切回来把这个任务做掉：

{% codeblock lang:bash %}
$ git checkout master
{% endcodeblock %}

3> 代码回到了之前的状态，先把小功能改完然后提交：

{% codeblock lang:bash %}
$ git commit -m "某个紧急问题"
$ svn commit -m "...."
{% endcodeblock %}

4> ok,去测吧。继续做newui

{% codeblock lang:bash %}
$ git checkout newui
{% endcodeblock %}

5> n久之后终于把newui做完可以提交svn了

{% codeblock lang:bash %}
$ git checkout master
$ git merge newui
$ svn commit -m "new ui"
{% endcodeblock %}

