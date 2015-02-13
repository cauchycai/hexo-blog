---
layout: post
title: "PHP初级面试问题整理"
description: ""
category: programming
tags: [php]
---
{% include JB/setup %}

## 简述面试者使用过的某一个框架？它的特性？ ##

MVC; Autoloading; Model; Logger;

## 面向对象特性的熟悉度 ##

多态是什么？ 单例模式是怎么实现的？abstract抽象类可以作什么用？

## Cookie 和 Session 的差别 ##

Session的用处； 二者保存在的位置不同； Session的有效期（浏览器关闭后失效）；

## PHP 中empty和isset的区别 ##

1. 对于empty

- 假如参数未声明，会报一个warning；
- { 0, 0.0, "0", "", NULL, 空数组, FALSE, 声明了但未赋值的变量, }

2. isset

- 声明过并且值不是NULL

## PHP 有哪些方法可以用来调试代码 ##

1. var\_dump和print\_r的差别

2. error log

## 有没有了解过PHP的一些编码规范 ##

PEAR; PSR2; ZEND;

1. 你在写代码时遵循哪一种规范？

## 正则表达式的掌握情况？ ##

/2015/02/12/name => _posts/2015-02-12-name.html

## 是否接触过Memcache ##

1. Memcache是什么？使用场景？

## 是否熟练使用 unix/linux 操作系统? ##

1. 文件权限的控制：

- 如何改变一个文件的owner (chown)
- 如何控制一个文件只能被owner访问 (chmod)
- 如何拷贝一个目录 (cp -Rf, rsync)

2. 管道是什么？

3. 检索一个错误日志可以使用哪些shell命令

## JS的熟悉程度 ##

1. 变量的作用域

2. jQuery: 如何找到一个dom对象的所有带class active的a子元素。

## 经常阅读哪些博客／网站? ##

考察面试者是否是爱好做技术这件事，以及他获取信息的来源是否是一些比较优质的资源。

## 喜欢阅读的技术书籍？举一些例子。 ##

同上。

## 简述你常用的开发工具，优点，为什么使用？ ##

了解面试者是否有提高自己开发效率的意识。

## 是否做过个人业余项目？ ##