---
layout: post
title:  "cocos2d-x的自适应布局系统"
date:   2016-05-10 09:51:02
categories: cocox2d-x layout widget
---

cocos2d-x的坐标系统

## widget组件

[参考](http://www.cocos.com/docs/creator/ui/widget-align.html)

* 在对齐策略里，widget组件是作为调整Node节点的size和xy存在的
* 在写好widget后，再进行修改位置或宽高会反应在widget里
* 如果使用下方的Horizontal Center的话，那么就会直接进行居中显示，但是size会自动变成40
* 如果左右同时定下来，那么素材的尺寸就会被定下来
