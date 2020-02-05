---
layout: post
title:  "haproxy"
date:   2016-10-20 09:51:02
categories: haproxy
---

## socat
测试下来，socat要比haproxy稳定，速度快，推荐使用

```shell script
nohup socat -T 600 TCP4-LISTEN:1883,reuseaddr,fork TCP4:54.223.43.113:1883  >> socat1883.log 2>&1 &
```



## deprecated under here

## haproxy

```shell script
yum install -y haproxy
```

```
# vi /etc/haproxy/haproxy.cfg
global
    # to have these messages end up in /var/log/haproxy.log you will
    # need to:
    #
    # 1) configure syslog to accept network log events.  This is done
    #    by adding the '-r' option to the SYSLOGD_OPTIONS in
    #    /etc/sysconfig/syslog
    #
    # 2) configure local2 events to go to the /var/log/haproxy.log
    #   file. A line like the following can be added to
    #   /etc/sysconfig/syslog
    #
    #    local2.*                       /var/log/haproxy.log
    #
    log         127.0.0.1 local2

    chroot      /var/lib/haproxy
    pidfile     /var/run/haproxy.pid
    maxconn     20480
    user        haproxy
    group       haproxy
    daemon

    # turn on stats unix socket
    stats socket /var/lib/haproxy/stats
    ulimit-n 51200

defaults
    mode                    tcp
    log                     global
    option                  dontlognull
    timeout connect         10s
    timeout client          1m
    timeout server          1m
    maxconn                 20480

frontend cono *:8388
default_backend cono

backend cono
  balance roundrobin
  server cono cono.tlightsky.com:8388 maxconn 20480
```

配置好之后

```shell script
/etc/init.d/haproxy restart
```