---
title:  "github socks5 proxy"
date:   2016-07-25
categories: github socke5 proxy
---

## github 代理

前置条件：本地1082端口有sokcs5代理。如果没有，请参考[如何使用docker快速搭建Shadowsocks服务器](http://tlightsky.github.io/docker/shadowsocks/2016/01/19/how-to-setup-shadowsocks-by-docker.html)

修改 /etc/ssh/ssh_config，
在尾部插入

```
Host github github.com
     Hostname github.com
     User git
     ProxyCommand /usr/local/bin/proxy-wrapper '%h %p'
```

修改文件/usr/local/bin/proxy-wrapper：

```
nc -x127.0.0.1:1082 -X5 $*
```
```
chmod +x /usr/local/bin/proxy-wrapper
```

## windows下设置
替换ProxyCommand部分
```
Host github github.com
     Hostname github.com
     User git
     ProxyCommand connect -H 127.0.0.1:1080 %h %p
```
