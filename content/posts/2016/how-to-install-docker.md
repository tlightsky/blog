---
layout: post
title:  "如何安装docker"
date:   2016-01-16 1:23:57
categories: docker
---


参考[docker官方教程](https://docs.docker.com/engine/installation/ubuntulinux/)

简略概括一下：

1. `sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D`
2. `curl -sSL https://get.docker.com/ | sh`

Log into Ubuntu as a user with sudo privileges.
This procedure assumes you log in as the ubuntu user.

```shell script

Create the docker group.

$ sudo groupadd docker

Add your user to docker group.

$ sudo usermod -aG docker ubuntu
```

Log out and log back in.
This ensures your user is running with the correct permissions.
