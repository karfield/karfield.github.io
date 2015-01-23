---
layout: post
title:  "Mac下的各种科学开发配置"
date:   2015-01-21 12:00:00
categories: usenotes
---

在国内写代码，必须得翻山越岭才能取到真经，本文就教你怎样配置代理环境使得自己的开发更为高效。

![tested](https://img.shields.io/badge/本文所述方法在Mac_OS_X_10.10-通过了验证-brightgreen.svg)

# 使用ShadowSocks
---

![tested](https://img.shields.io/badge/推荐的ShadowSocksX版本:-2.6.2-0088ff.svg)

ShadowSocks貌似是目前最流行的加密代理，不同于VPN、OpenVPN等等，它配置简单轻量，在Mac下基本上不需要多少配置就可轻松科学上网。有了它，足以应付多数番茄需求了。

Mac使用ShadowSocks(以下简称SS)代理来上网极为简单, 分两步:

1. 下载 [ShadowsocksX客户端](https://sourceforge.net/projects/shadowsocksgui/)
2. 安装启动之后配置SS服务器的账号密码, 登入之后即可科学上网

**SS客户端配置**

官方默认配了Public Server, 但免费的总是堵的. 如果你要搭建自己的SS服务器, 可以参考 [搭建SS服务器]().

 **~/.ShadowsocksX/gfwlist.js**

这个是PAC配置文件,里面包含了需要自动代理的域名, 在domains中添加你想要的翻的域名或者子域名即可:

<pre>
```
var domains= {  
  "<domain-you-want-to-be-proxied>.com": 1,  
  //...  
}  
```
</pre>

**SS的本地SOCKS5端口: 1080**

在~/.ShadowsocksX/gfwlist.js文件中的proxy变量可以指定本地的代理端口(**默认: 1080**), 你可以参考`var proxy`修改成你想要的端口号

# 使用proxychains进行命令代理
---

proxychains是TCP和DNS的隧道工具（以下称这类工具为穿越工具）。只要在你执行命令之前添加*proxychains4 -g*即可以为该命令所用到的TCP连接进行代理。

proxychains支持多个代理服务器，所以如果头号代理服务器不行，后面会依次尝试别的服务器。

**安装:**

```
$ brew install proxychains-ng
```

装完之后执行的命令不是proxychains-ng，而是proxychains4


**配置proxychains**

在使用proxychains需要添加或修改一下配置文件：**~/.proxychains/proxychains.conf**，我的配置:

```
strict_chain
proxy_dns
remote_dns_subnet 224
tcp_read_time_out 15000
tcp_connect_time_out 8000
localnet 127.0.0.0/255.0.0.0
quiet_mode
[ProxyList]
socks5  127.0.0.1 1080
```

proxychains安装之后,即可愉快刷玩了:

```
$ proxychains4 -q program_name [arguments]
```

`-q`参数是quiet的意思, 加了就不会有Proxychains的打印; 还可用过-f <config_file_path>来使用指定的配置文件进行代理.

比如使用代理用wget下东西,可以这样:

```
$ proxychains4 -q wget http://www.google.com/
```

# 为ssh设置代理

在访问某个SSH主机时如果被墙，可以通过修改**~/.ssh/config**文件, 在某个Host字段下添加**ProxyCommand**的方式来做，比如

```
Host github.com
    ...
    ProxyCommand /usr/local/bin/corkscrew 127.0.0.1 1080 %h %p
    ...
```

这里的**corkscrew**是代理穿越工具之一，可以通过homebrew来安装. 相同值得推荐的还有proxytunnel，相应的配置需要修改成


```
Host github.com
    ...
    ProxyCommand /usr/local/bin/proxytunnel -q -p 127.0.0.1:1080 -d %h:%p
    ...
```

proxytunnel还支持设定UA(User Agent), 具体可以参考[这里](http://sun.hasenbraten.de/~frank/docs/proxytunnel.html)

# 为git设置代理
---

```
$ git config --global http.proxy 'socks5://127.0.0.1:1080'
$ git config --global https.proxy 'socks5://127.0.0.1:1080'
```

# 为maven设置代理
---

