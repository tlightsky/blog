---
layout: post
title:  "animatron动画库分析"
date:   2016-01-28 09:51:02
categories: animation react
---

[animatron][animatron]的动画库，当前的develop branch其实是不合适做研究的，
先切换到v1.5的branch：

```shell
git checkout tags/v1.5
```

在整理的时候，需要先有一个清晰的思路，即：
动画是由素材与素材的行为组成的。
在时间线上，素材在不同的时间点展现出不同的变换，最终呈现出动画的效果。

### 时间线的移动
在`render/r_loop`中，不断请求下一次渲染继续调用`render/r_loop`。
在每次迭代中，通过`render/r_at`来实现更新内容。
最终，通过`anim.render`这个函数来实现整个anim的重绘。

### 时间tick中，动作的管理
`anim/render`其实是委托给了`element/render`，因为anim其实主要是由element组成的。
而在`element/render`的render过程中，最重要的是`element/modifiers`，
这个抽象概念，是一次渲染过程中的改变器。
分为`C.MOD_SYSTEM, C.MOD_TWEEN, C.MOD_USER, C.MOD_EVENT`这么多不同的种类。
其中，`Tween`是所有基本动作的改变发生的地方。
而`Event`是所有事件触发的方式。

### Tween的生产
所有的Tween都是从Importer中产生的，在import的过程中，
根据`Tween/register`注册的不同函数。

### Immutable的展望
从Immutable的角度来看动画的话，
可以简单的理解为 `state[time] = f(initialState, time)` 的数组。
同时，由于这种迭代的模式，其实可以通过`dp`的方式，减少数据结构的浪费。



[animatron]: https://github.com/Animatron/player
