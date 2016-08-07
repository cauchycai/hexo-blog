---
title: "git-svn 的使用"
date: 2015-05-25 00:00:00
tags: [git, software]
---


团队用了很多年的svn，短时间内看不到切换到git进行版本管理的可能。

svn当然足够用了。可惜用过git之后就不再这么觉得。

分布式带来的离线提交的好处倒是其次。关键是git让我喜欢branch，你能想象在svn里面每天几次进行branch切换和merging吗？ 有了branch之后，开发流程管理变得简单了。只有当一个功能准备上线时才将这个功能分支 merge 到 master 分支。这样就保证了一个功能尚未完成时永远不影响 线上版本（master）的小版本更新。

所以我的开发环境使用 git，用 git-svn 这个工具提交代码到 svn 版本库。

具体的流程是这样：

#### 1. 检出 svn 版本库 ####

{% codeblock bash %}
$ git svn clone http://svn.repo.url/project
{% endcodeblock %}


#### 2. 本地有了一个 git 库，里面有所有 svn 历史提交，并且有一个特殊的 remote 分支叫做 git-svn 。可以用下面这个命令查看。 ####

{% codeblock bash %}
$ git branch -a
{% endcodeblock %}

#### 3. O.K. 现在本地是 git 库了，你就像使用其他 git 项目一样的使用它，甚至你可以添加其他 remote 。当你想把代码提交到 svn 。 ####

{% codeblock bash %}
$ git svn dcommit
{% endcodeblock %}

这个命令会把当前 git 分支的最近一次 commit 提交到 git-svn 这个 remote 分支，并且 push 到 svn 服务器。


#### 4. 那 svn up 用什么代替？ 用这个命令： ####

{% codeblock bash %}
$ git svn rebase
{% endcodeblock %}

O.K. 这样就可以满足大部分的使用场景了。

相关的文档可以看这里： https://www.kernel.org/pub/software/scm/git/docs/git-svn.html
