---
layout: post
title:  "如何使用docker快速搭建Shadowsocks服务器"
date:   2016-01-19 09:51:02
categories: docker shadowsocks
---

### 前置条件：

* [安装docker](http://tlightsky.github.io/docker/2016/01/16/how-to-install-docker.html)
* [安装docker-compose](http://tlightsky.github.io/docker/docker-compose/python/pip/2016/01/16/how-to-install-docker-compose.html)

### 搭建方法：

* 将 [docker-shadowsocks-python][docker-shadowsocks-python] clone到本地。
* 新建shadowsocks配置文件：

```shell script
mkdir conf
vim conf/shadowsocks.json
```

配置文件示例：
```json
{
 "server":"0.0.0.0",
 "local_port":1080,
 "server_port":8388,
 "password":"MyPowerfulPassword",
 "timeout":300,
 "method":"aes-256-cfb"
}
```

* 编写docker-compose.yml文件：

```shell script
ssp:
  build: .
  ports:
   - "8388:8388"
  volumes:
   - ./conf:/etc/shadowsocks
  restart: always
```

* docker-compose up -d

[docker-shadowsocks-python]: https://github.com/WhiteWorld/docker-shadowsocks-python
