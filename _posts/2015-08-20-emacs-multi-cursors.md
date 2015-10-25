---
layout: post
title: "My Favourite Emacs Modes - multiple-cursors"
description: ""
tags: [emacs]
---


### multiple-cursors 解决的问题 ###

通常编辑一个文件时只有一个光标（输入的位置）。multiple-cursors 实现了同时有多个光标，输入同时在这多个光标处发生。

### 如何安装 ###

{% highlight lisp %}
(require-package 'multiple-cursors)
{% endhighlight %}

### 常用命令 ###

C-> => mc/mark-next-like-this, 寻找下一个与当前“选中”（region） 相匹配的文本并选中匹配并添加新光标；

C-< => mc/mark-next-like-this, 类上，但是寻找方向相反；

C-c C-< => mc/mark-all-like-this, 找到当前buffer中所有匹配并增加光标；

完成编辑后按 <return> C-g 结束编辑，如果需要在multiple-cursors状态下输入换行，须使用 C-j, 因为 <return> 会结束编辑。

### 对多行的region的操作 ###

C-c c c => mc/edit-lines, 当前选中的region中的每一行增加一个cursor；

C-c c e => mc/edit-ends-of-lines, 当前选中的region中的每一行的行尾增加一个cursor；

C-c c a => mc/edit-beginnings-of-lines, 当前选中的region中的每一行的行首增加一个cursor；

### 其他 ###

mc/mark-all-in-region

mc/mark-all-like-this-in-defun

mc/mark-all-symbols-like-this-in-defun

mc/insert-numbers

mc/sort-regions

mc/reverse-regions
