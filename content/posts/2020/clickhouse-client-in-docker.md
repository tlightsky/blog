---
title: "Clickhouse Client in Docker"
date: 2020-02-29T15:26:41+08:00
draft: false
---

通过配置文件进行连接的方式：

```shell
docker run -it  -v $HOME/.clickhouse-client/oldch.xml:/root/.clickhouse-client/config.xml yandex/clickhouse-client
```

当然也可以直接运行这个client的命令：

```shell
docker run -it yandex/clickhouse-client
```

如果不要compression，可以这么传：

```shell
docker run -it yandex/clickhouse-client --compression=0
```
