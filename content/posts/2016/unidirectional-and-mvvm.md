---
layout: post
title:  "Unidirectional and MVVM"
date:   2016-10-10 09:51:02
categories: Unidirectional MVVM react vue
---

## Unidirectional

数据部分完全决定界面的显示内容，
任何部分数据变动，都自动进行界面改变


## MVVM

展示数据部分与变量双向绑定，
界面内数据变化可以迅速反馈到数据，
坏处是，有部分非界面数据无法参与绑定，
此类数据改变后也不会自动出发界面更替
