---
layout: post
title: "Moco"
description: ""
tags: [moco]
---
{% include JB/setup %}

# 解决的问题 #

Moco是一个用来模拟外部服务器的工具。在系统集成时，外部接口的稳定性无法在我们的掌控中，使用这个工具就可以弥补这个问题，即使外部接口不可用也不影响我们自己系统的开发和测试。

# 安装 #

下载：http://repo1.maven.org/maven2/com/github/dreamhead/moco-runner/0.10.0/moco-runner-0.10.0-standalone.jar

运行：

{% highlight bash %}
$ java -jar moco-runner-<version>-standalone.jar http -p 12306 -c foo.json
{% endhighlight %}


这样就启动一个moco实例，在12306端口接受http请求。foo.json作为配置文件，决定这个模拟服务器如何响应请求。


# json格式配置文件 #

每一个moco实例对应一个这样的配置文件。

配置举例：

1. URI

{% highlight json %}
{
  "request" :
	{
	"uri" : "/foo",
	"queries" :
		{
		  "param" : "blah"
		}
	},
  "response" :
	{
	  "text" : "bar"
	}
}
{% endhighlight %}

测试，通过浏览器访问：http://localhost:12306/foo?parm=blah


2. URI with HTTP method; URI regular expression match

{% highlight json %}
{
  "request" :
	{
	  "method" : "get",
	  "uri" : {
		"match": "/\\w*/foo"
	  }
	},
  "response" :
	{
	  "text" : "bar"
	}
}
{% endhighlight %}

3. json response

{% highlight json %}
{
	"request" :
	{
		"uri" : "/sns/oauth2/access\_token?appid=APPID&secret=SECRET&code=CODE&grant\_type=authorization\_code"
	},
	"response" :
	{
		"json" :
		{
			"access\_token":"aaaaaaaaaaaaaaaaaaaaaaaaa",
			"expires\_in":7200,
			"refresh\_token":"rrrrrrrrrrrrrrrrrrrrrrrrr",
			"openid":"o-MCxjgmz73EWpfb86ls38LHicdc",
			"scope":"SCOPE"
		}
	}
}
{% endhighlight %}


4. Redirect

{% highlight json %}
{
	"request" :
	{
		"uri" : "/redirect"
	},
	"redirectTo" : "http://www.guanaitong.com"
}
{% endhighlight %}


# 如何在测试/开发环境部署 #

如果外部测试服务器域名为：api.thirdparty.com

1. 在某端口（如12306）运行模拟服务器实例

{% highlight bash %}
$ java -jar moco-runner-<version>-standalone.jar http -p 12306 -c foo.json
{% endhighlight %}


2. 在web服务器（nginx）配置中设置反向代理

{% highlight nginx %}
server {
	listen 80;
	server\_name api.thirdparty.com;
	location / {
		proxy\_set\_header   X-Real-IP $remote\_addr;
		proxy\_set\_header   Host      $http_host;
		proxy\_pass         http://127.0.0.1:12306;
	}
}
{% endhighlight %}

3. 修改测试开发环境对于api.thirdparty.com的域名解析，使其指向测试/开发服务器。

4. 之后调用第三方接口就是使用模拟服务器了
