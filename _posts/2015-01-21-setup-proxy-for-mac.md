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

Mac使用ShadowSocks(以下简称SS)代理来上网极为简单, 分两步:

1. 下载 [ShadowsocksX客户端](https://sourceforge.net/projects/shadowsocksgui/)
2. 安装启动之后配置SS服务器的账号密码, 登入之后即可科学上网

**SS客户端配置**

官方默认配了Public Server, 但免费的总是堵的. 如果你要设置自己的SS服务器, 可以参考 [配置SS服务器]().

 **~/.ShadowsocksX/gfwlist.js**

这个是PAC配置文件,里面包含了需要自动代理的域名, 在domains中添加你想要的翻的域名或者子域名即可:

```
var domains= {<br>
  "<domain-you-want-to-be-proxied>.com": 1,
  //...
}
```

**SS的本地SOCKS5端口: 1080**

在~/.ShadowsocksX/gfwlist.js文件中的proxy变量可以指定本地的代理端口(**默认: 1080**), 你可以参考`var proxy`修改成你想要的端口号

# 安装proxychains以便在终端中使用代理
---

**使用homebrew安装:**

```
$ brew install proxychains-ng
```

**配置proxychains**

配置文件: **~/.proxychains/proxychains.conf**

我的配置:

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

proxychains-ng安装之后,对应的具体命令是**proxychains4**. 对于该命令的使用方式:

```
$ proxychains4 -q program_name [arguments]
```

`-q`参数是quiet的意思, 加了就不会有Proxychains的打印; 还可用过-f <config_file_path>来使用指定的配置文件进行代理.

比如使用代理用wget下东西,可以这样:

```
$ proxychains4 -q wget http://www.google.com/
```

# 为git设置代理
---

# 为maven设置代理
---

