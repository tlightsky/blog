---
layout: post
title:  "cljs获取函数回调参数的方法"
date:   2016-05-12 09:51:02
categories: laravel controller
---

## callback argument as chan
`<<<` 这种方法是可以的
`<<obj` 是之前我自创的，试用宏的方式获得chan


## 排序，(sort-by keyfn list)

```clojure
(defonce keyfy-re #".*_(\d+)\.jpg")

(defn keyfy [s]
  (let [s (second (re-find keyfy-re s))]
    (js/parseInt s)))
```

## 合并多个bmp文件

```clojure
(defn frame-path [i]
  (let [prefix (str droot sep "tmp" sep "screen" sep)]
    (str prefix "frame" i ".bmp")))

(defn join-bmp [bmps]
  (let [bmp-datas (map #(->> % (.readFileSync fs) (.decode bmp)) bmps)
        bmp-datas (js->clj bmp-datas)
        _ (debug :json "join-bmp" ((-> bmp-datas first) "width"))
        one-bmp (reduce
                 (fn [x y]
                   {"data" (.concat js/Buffer (clj->js [(x "data") (y "data")]))
                    "width" (x "width")
                    "height" (+ (x "height") (y "height"))}) bmp-datas)
        one-bmp-data (->> one-bmp clj->js (.encode bmp))
        one-bmp-data (.-data one-bmp-data)
;;         _ (debug :json "join-bmp" one-bmp-data)
        one-bmp-path (first bmps)
        _ (.writeFileSync fs one-bmp-path one-bmp-data)]
    [one-bmp-path]))
```

## jstr->clj-origin
之前在jstr->clj里做了处理，可以都以 :key
但是这个处理有bug，不能做多层级处理
不能很好的处理数组
所以要用origin来处理这些情况
那在用origin时就是能以这种形式来获取内容了：
```clojure
(obj "key")
```

PS: 昨天干了一个很蠢的事，在调研清楚功能之前先选用库进行调试。
做了一些无用功，这点需要自省，在做之前掌握所有信息。
对所有观点进行压力测试，找最聪明的人反驳自己，以接近真实。
