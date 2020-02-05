---
layout: post
title:  "类似background-size:cover的缩放算法"
date:   2016-05-30 09:51:02
categories: background-size cover scale image
---

## css中background-size: cover的缩放
简单的说，就是一边match，另外一边超出后剪裁的适配方案
现在需要适配视频到屏幕上，保持`高宽比`和`无黑边`比较重要，
所以选择这个方案

## 算法实现
参考[这里](http://stackoverflow.com/questions/10285134/whats-the-math-behind-csss-background-sizecover)
