---
layout: post
title:  "cocos2d-x系统搭建与学习"
date:   2016-05-04 09:51:02
categories: cocox2d-x
---

最近在调研cocos-x平台，是否可以搭建自适应动画平台。

## 下载搭建系统

```shell script
git clone git@github.com:cocos2d/cocos2d-x.git tags/cocos2d-x-3.10 -b cocos2d-x-3.10
cd cocos2d-x
python download-deps.py
git submodule update --init
cd cocos2d-x
./setup.py
source FILE_TO_SAVE_SYSTEM_VARIABLE
cocos new MyGame -p com.your_company.mygame -l cpp -d NEW_PROJECTS_DIR
cd NEW_PROJECTS_DIR/MyGame
```

PS:这里犯蠢了，没有仔细看介绍，走了一些弯路

## cocos系统介绍
[这里](http://www.cocos.com/doc/article/index?type=cocos2d-x&url=/doc/cocos-docs-master/manual/framework/native/v3/basic-concepts/zh.md)有一个整体的框架图，我觉得画的还不错，可以作为概念的入门。

## 创建游戏
直接参照github上的流程就可以跑了。

```shell script
cocos run -p ios
```

## 调研
最近考虑给予cocos搭建LED平台，
需要调研的有两个点：

* 是否支持搭建无缝式开发发布平台
* 如何进行自适应开发，适应不同的屏幕

## Creator
这是由cocos2d-x推出的所见即所得的编辑器，
使用方式非常类似unity3d

这种情况下，script其实是挂在到组件上的，可以用getComponent上拿到挂载的脚本

同样是通过树形来组织整动画结构

现在唯一可能有些疑惑的是prefab的机制是什么样的

## 星星游戏

这个游戏比较简单，

### Game.js
这里是游戏的主脚本，挂载在canvas上，
产生初始的星星，进行游戏终结的判断

### Star.js
这里主要是判断星星的距离是否足够近，就收集星星并产生新星星

### Player.js
这里是对玩家对象的操控，对按键的反馈

## Prefab
[Prefab](http://www.cocos.com/docs/creator/asset-workflow/prefab.html)

## Node与Sprite的关系

[参考这里](http://www.cocos.com/docs/creator/content-workflow/node-component.html)

![Node与Sprite的关系](http://www.cocos.com/docs/creator/content-workflow/node-component/node_chart.png)

## CC类的使用方法
[CCClass](http://www.cocos.com/docs/creator/scripting/reference/class.html)

## 节点关系

![节点关系](http://www.cocos.com/docs/creator/content-workflow/node-tree/2dx-node-tree.png)

## 布局与对齐

[布局与对齐](http://www.cocos.com/docs/creator/ui/widget-align.html)
