---
layout: post
title:  "如何使用docker搭建简易ftp服务器"
date:   2016-01-16 5:23:57
categories: ftp docker pure-ftp
---

本篇讲述如何使用docker快速搭建ftp服务器。

### 前置条件：

* [安装docker](http://tlightsky.github.io/docker/2016/01/16/how-to-install-docker.html)
* [安装docker-compose](http://tlightsky.github.io/docker/docker-compose/python/pip/2016/01/16/how-to-install-docker-compose.html)


### 搭建方法：

使用[stilliard/pure-ftpd](stilliard/pure-ftpd)，这个ftp docker image。
步骤如下：

* 新建ftp/docker-compose.yml文件，内容在下方



```yaml
ftp:
  image: stilliard/pure-ftpd
  volumes:
    - "./app:/home/ftpusers/code"
    - "./pure-ftpd:/etc/pure-ftpd"
  ports:
    - "21:21"
    - "30000:30000"
    - "30001:30001"
    - "30002:30002"
    - "30003:30003"
    - "30004:30004"
    - "30005:30005"
    - "30006:30006"
    - "30007:30007"
    - "30008:30008"
    - "30009:30009"
  environment:
    PUBLICHOST: localhost
```

* 新建app文件夹，并`chmod 777 app`
* 在ftp目录中，运行`docker-compose up -d`
* 运行命令`docker exec -it ftp_ftp_1 bash`，进入docker容器内部
* 建立用户：

```shell script
pure-pw useradd code -u ftpuser -d /home/ftpusers/code
pure-pw mkdb
```


完成后就可以访问ftp服务了



[stilliard/pure-ftpd]: https://hub.docker.com/r/stilliard/pure-ftpd/
