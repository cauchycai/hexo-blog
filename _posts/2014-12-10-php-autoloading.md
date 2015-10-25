---
layout: post
title: "PHP Autoloading"
description: ""
tags: [php]
---


# 解决的问题 #

Autoloading机制是php5引入的特性。
一个类的实现可能需要依赖很多其他类，这就需要要么在脚本开始的地方引用所有基础类，要么在每个类的地方手动写上很长的一段类的引用。
使用autoloading可以利用php运行环境来自动引用需要的类文件。

使用上主要是用到了__autoload函数或者 spl\_autoload\_register

# spl_autoload_register #

支持多个autoload方法/函数, 多个不同autoload方法可以用来支持自动require多个不同目录位置的类。

## 类方法作为注册为autoload函数 ##

{% highlight php %}
class Autoloader
{
	private $dir;
	public function __construct($dir = null)
	{
		if (is_null($dir)) {
			$dir = dirname(__FILE__).'/..';
		}
		$this->dir = $dir;
	}
	public static function register($dir = null)
	{
		ini_set('unserialize_callback_func', 'spl_autoload_call');
		spl_autoload_register(array(new self($dir), 'autoload'));
	}
	public function autoload($class)
	{
		if (file_exists($file = $this->dir.'/'.str_replace('\\', '/', $class).'.php')) {
			require $file;
		}
	}
}
{% endhighlight %}

## 具体使用 ##

{% highlight php %}
require_once PATH_TO_AUTOLOAD_CLASS;
$loader = new Autoloader();
$loader->register(HELPER_PATH);
$loader->register(MODEL_PATH);
{% endhighlight %}

# psr-4 #

"PHP Framework Interop Group" 这个组织定义的Autoloading实现规范。

http://www.php-fig.org/psr/psr-4/

## 合法的类名 ##

	\<NamespaceName>(\<SubNamespaceNames>)*\<ClassName>

1. 必须有一个顶级namespace, 这个namespace也被称为 "vendor namespace";
2. 可以有一个或多个 sub-namespace;
3. 结尾处必须有一个类的名字
4. 下划线(_)没有特殊的意义(不同于psr-0)
5. 名字中大小写组合无限制
6. 字母大小写敏感

## 根据类名来选择include哪个php文件 ##

1. 顶级namespace对应到一个base目录
2. sub-namespace逐级对应base目录下的子目录
3. 结尾处类名对应到<ClassName>.php文件

# 使用autoloading的坏处 #

没法显示的看到require的顺序，给调试带来不便。
