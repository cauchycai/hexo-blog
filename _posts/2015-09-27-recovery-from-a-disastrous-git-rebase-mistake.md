---
layout: post
title: "Git-rebase 误操作的恢复"
description: ""
tags: [git]
---


我在进行一个 Git 的常用操作 - rebase 时，遇到了一个致命错误，导致开发分支上的commit丢失。慌张的同时，由于相信 Git 提供了保险措施，我找到了恢复丢失的 commit 的方法。这里记录一下。

我进行的这个 rebase 操作是 Git 分支管理中很常见的一个操作：

我在一个分支上做一个 feature 的开发，这个分支叫做：oauth2-login。另外有 master 分支与预发布的分支同步。当有一个功能需要快速开发并上线时，我会切换到 master 分支进行代码编写并合并到预发布分支，然后切换回当前的开发分支：oauth2-login。切过去之后需要将 master 的最新修改合并到 oauth2-login ，使用 git rebase master 来实现。当 rebase 时遇到冲突，需要将这些冲突的地方手动 fix， 并且 git add 然后 git rebase --continue。但是假如最后一步 没有用 continue， 而是用了 git rebase --skip，那就完蛋了，所有开发分支上未合并到 master 的 commit 统统丢失。

这里就记录下丢失后如何找回。

Git 并不会真的将那些已删除的commits从它的数据中删除，所以我的那些被不小心删除的commits仍旧保存在 Git 的数据文件中，在某个地方，我只需要把它们找出来。

首先，需要查看 .git/logs/refs 目录， 在它下面会看到两个目录 heads 和 remotes。我们需要进入 .git/logs/refs/heads, 因为 remotes 保存的是 remote branch 的信息。在 .git/logs/refs/heads/ 目录下会看到一些和分支同名的文件。找到我操作的分支: oauth2-login, 打开查看其中内容。

此文件中保存了我在此分支上的操作记录，也包括了我最近的那次rebase，从操作前head 对应的 commit 的 sha1 到 rebase 之后 head 对应的 commit 的 sha1 。
那接下来的操作就变得十分简单：

    $ git checkout -b oauth2-login-recovery foiwjfelajwldfj913s

这个操作会以我rebase之前的head为base新建一个 branch，这个branch就包含了我所有丢失的commits。这样丢失的数据就找回来了。
