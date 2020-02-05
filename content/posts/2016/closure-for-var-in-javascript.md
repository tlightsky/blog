---
layout: post
title:  "closure for var in javascript"
date:   2016-10-24 09:51:02
categories: javascript
---

## clojure
```clojure
(function (a) {
  return function () {
    console.log(a);
  }
})("arg");
```
## bind
```clojure
(function (a) { console.log(a); }).bind("arg");
```
