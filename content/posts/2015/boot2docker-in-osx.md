---
title:  "boot2docker在Mac中跑web可能遇到的问题"
date:   2015-12-04
categories: docker boot2docker mac
---
在Mac中使用docker，需要boot2docker这个工具。

它其实是借助virtualbox跑了一个linux虚拟机。

所以在使用上会与linux上的docker有些不同。

最近遇到的一个大坑就是：

**如果你在boot2docker中，使用port选项指定了一个端口。
其实不是指映射到你本地Mac的端口，而是映射到virtualbox的端口。**

比如docker-compose里，指定端口映射`port: "80:80"`

此时，直接打开Mac的`localhost:80`是没法打开web页的

需通过boot2docker ip这个命令，得到虚拟机的ip地址。直接打开这个ip地址就能打开web页。

也就是说，此时这个80的端口实际上是绑定到了虚拟机的80端口而非本地Mac的80端口。

PS：
新版本的Docker Desktop已经没有这个坑了，直接映射的本地端口