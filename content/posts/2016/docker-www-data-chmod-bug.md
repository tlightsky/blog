---
layout: post
title:  "Docker挂载的Volume，无法在内部改变目录权限的问题"
date:   2016-03-24 09:51:02
categories: php docker chmod www-data volume vbox
---

# 问题

这两天在调试phalcon的时候遇到一个问题

使用[百度的前端编辑器](http://ueditor.baidu.com/)

它会自动创建目录，并修改目录权限为777

# 现象

一般来说这样是没有问题的

但是尝试了几次，都发现，只能创建755的目录

# 原因

最终在stackoverflow上找到了答案：

由于目录是用docker挂载的，而boot2docker跑在virtualbox的虚拟机中，使用的是virtualbox的挂载方法

而vbox的挂载是不支持目录权限的

所以就没法在container内部修改了

# 办法

最终在Mac上，手动把权限改了就好使了
