---
title: "OSX 上的 VPN 环境配置指南"
date: 2015-11-05 00:00:00
tags: [vpn, gfw, osx]
---

使用 VPN 主要是为了能正常访问被防火墙屏蔽的网站。

但是在开发环境中并不希望所有IP段的访问都走VPN线路。所以使用VPN的情况有以下几个问题需要解决。

1. 测试/开发环境的domain要被测试/开发环境的DNS服务器解析
2. 避免测试/开发环境的domain走内网网关
3. 国内网站使用不走VPN线路

关于问题1。 可以通过设置VPN网络连接所使用的dns服务器来修改。

关于问题2。OSX 上会自动做这个设置，内部网络 10.x.x.x 或 192.168.x.x 网段会自动连到本地网络的网关。但是如果测试环境并不在这些网段则需要在 /etc/ip-up 和 /etc/ip-down 中分别加入:

{% codeblock bash %}
route add xxx.xxx.xxx.0/24 "zzz.zzz.zzz.zzz"
route add yyy.yyy.0.0/16 "zzz.zzz.zzz.zzz"
{% endcodeblock %}

和

{% codeblock bash %}
route delete xxx.xxx.xxx.0/24 "zzz.zzz.zzz.zzz"
route delete yyy.yyy.0.0/16 "zzz.zzz.zzz.zzz"
{% endcodeblock %}

这里假设本地网络网关地址是 zzz.zzz.zzz.zzz


关于问题3。可以使用chnroutes： https://code.google.com/p/chnroutes/ ，或这里  https://github.com/alsotang/ppp
