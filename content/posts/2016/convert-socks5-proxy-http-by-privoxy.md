---
layout: post
title:  "convert sokcs5 proxy http by privoxy"
date:   2016-7-30 09:51:02
categories: sockes http proxy privoxy
---

## privoxy

安装privoxy
```shell script
brew install privoxy
```

编辑配置文件
`vi ~/config`

```shell script
listen-address 0.0.0.0:1080
forward-socks5 / localhost:1082 .
```


运行
```shell script
/usr/local/Cellar/privoxy/3.0.24/sbin/privoxy
```
