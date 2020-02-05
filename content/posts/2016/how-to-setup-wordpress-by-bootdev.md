---
layout: post
title:  "如何使用bootdev的php docker脚本，快速搭建一个wordpress"
date:   2016-01-16 4:23:57
categories: wordpress bootdev
---

### 预置条件：

* [数据库搭建](http://tlightsky.github.io/wordpress/mysql/linux/2016/01/16/how-to-install-mysql-server.html)
* [安装docker](http://tlightsky.github.io/docker/2016/01/16/how-to-install-docker.html)
* [安装docker-compose](http://tlightsky.github.io/docker/docker-compose/python/pip/2016/01/16/how-to-install-docker-compose.html)


### 搭建方法：


* 将bootdev的[phpfpm][phpfpm]项目clone到本地
* 在根目录下编写`docker-compose.yml`如下：

```yaml
web:
  build: .
  ports:
    - "80:80"
  volumes:
    - ./app:/usr/local/nginx
```

* 下载并解压wordpress文件，并命名为app目录：

```shell script
wget http://wordpress.org/latest.zip
unzip latest.zip
mv wordpress app
```

* 修改数据库配置wp-config.php


另外想要用好wordpress，一个ftp配置会是很方便的选择。
可以参考我的另外一篇，[如何使用docker搭建简易ftp服务器](http://tlightsky.github.io/ftp/docker/pure-ftp/2016/01/16/how-to-setup-ftp-by-docker.html)


[phpfpm]: https://github.com/chankongching/bootdev-nginx-phpfpm56-docker
