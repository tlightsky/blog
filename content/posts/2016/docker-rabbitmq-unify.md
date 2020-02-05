---
layout: post
title:  "rabbitmq的docker内外统一化"
date:   2016-07-20 09:51:02
categories: video template
---

# 目标
最近要对docker集群进行动态扩展，
这样之前使用的本地rabbitmq就需要变成中心rabbitmq才行了，
总之程序内先设置连接到rabbitmq`(str "amqp://" username ":" password "@rabbitmq:5672")`

# 连接docker内的rabbitmq
在rabbitmq官方提供的docker镜像中，
可以设置默认用户名与密码，
在docker-compose里设置一下即可：

```yaml
rabbitmq:
  image: rabbitmq
  environment:
   - TZ=Asia/Shanghai
   - RABBITMQ_DEFAULT_USER=username
   - RABBITMQ_DEFAULT_PASS=password
```

另外需要link一下：
```yaml
links:
 - redis
 - rabbitmq
```


# 连接docker外的rabbitmq
首先，使用外部的rabbitmq时links，
需要为container设置rabbitmq的hosts地址。

```yaml
extra_hosts:
 - "rabbitmq:162.242.195.82"
```


[compose-file](https://docs.docker.com/compose/compose-file/)
