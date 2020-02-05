---
layout: post
title:  "什么是Jsonp"
date:   2016-01-14 11:23:57
categories: javascript jsonp
---

jsonp是实现跨站ajax的一种手段。

使用方法是：

1. 定义好接收数据的callback
2. 新插入script标签，并将src指向非同源的url，同时url参数中附上callback的名字

加载的script内容类似于下面：

```html
<script>
callback('ajax data')
</script>
```

这样当新插入的标签会自动调用callback并以ajax data作为参数。

由于script的src是没有同源限制的，所以使用这个方法可以绕开这个条件实现跨站加载。
