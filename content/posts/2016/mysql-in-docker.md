---
layout: post
title:  "mysql in docker"
date:   2016-10-30 09:51:02
categories: javascript
---


### 前置条件：

* [安装docker](http://tlightsky.github.io/docker/2016/01/16/how-to-install-docker.html)
* [安装docker-compose](http://tlightsky.github.io/docker/docker-compose/python/pip/2016/01/16/how-to-install-docker-compose.html)


## mysql in docker
```yaml
mysql:
  image: mysql/mysql-server
  ports:
    - "9527:3306"
  environment:
    - MYSQL_ROOT_PASSWORD=MyRootPassword
    - MYSQL_USER=great
    - MYSQL_PASSWORD=GreatPassword
  volumes:
    - "./datadir:/var/lib/mysql"
```