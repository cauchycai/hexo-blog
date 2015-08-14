---
layout: post
title: "My Favourite Emacs Modes - 1. Projectile"
description: ""
tags: [emacs]
---
{% include JB/setup %}

### Projectile 解决的问题 ###

通常我们写程序时会同时打开几个项目，在不同项目的代码文件之间跳来跳去。Projectile 实现了快捷的查找项目内文件或另一项目内的文件。另外还能实现项目内 grep。

### 如何使用 ###

对于被 version control 了的项目，不需要做任何配置 Projectile 即可识别并以版本库为单元区分项目。

假如一个项目还没有版本控制，那我们可以在项目的根目录下创建 .projectile 这样一个空白文件，于是这个目录就被 projecctile 识别为项目根目录。

### 常见 command ###

C-c p f => projectile-find-file, 查找当前文件项目的一个文件。

C-c p p => projectile-switch-project, 切换项目并查找那个项目中的文件。

C-c p b => projectile-switch-to-buffer, 切换到项目内某一个 buffer。 假如不用 projectile，我们只能用 C-x b 切换buffer， 这时候提供候选的buffer会包含所有emacs打开了的buffer（最近使用的排在前面），那经常的我们只想切换到本项目内最近打开的某个buffer，假如用 C-x b 则多了很多干扰。

C-c p I => projectile-ibuffer, 查看项目中打开了哪些buffer，并对某些buffer进行操作。

C-c p ! => projectile-run-shell-command-in-root, 在项目根目录处运行一个shell命令。

C-c p & => projectile-run-async-shell-command-in-root, 异步运行shell命令。

C-c p S => projectile-save-project-buffers, 保存本项目中所有打开的buffer。

C-c p k => projectile-kill-buffers, 关闭本项目中所有打开的buffer。

C-c p r => projectile-replace, 项目中批量替换文本。

C-c p s g => projectile-grep, 项目中grep。

C-c p 4 f => projectile-find-file-other-window, 在项目中查找文件并在另一个window中打开。
