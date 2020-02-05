---
layout: post
title:  "sql cte with"
date:   2019-05-20 09:51:02
categories: sql with cute
---

# SQL Withfy

## 改造方案遇到困难

尝试对python parser和tidb parser改造，

遇到了困难，

- python parser是基于generator的，想要机遇ast进行修改替换内容相对比较困难
- tidb的parser是严格兼容Mysql语法的，想要做一套一并兼容mysql和clickhouse的方案比较困难

正好碰到另外一个[自写parser的解决方案](https://github.com/sql-machine-learning/sqlflow/blob/develop/doc/sql_parser.md)，

于是决定还是使用自写parser这种方案



## 自写parser方案

目前想到的是可以使用[goyacc](https://www.epaperpress.com/lexandyacc/download/yacc.pdf)来解析大的SELECT组件，

然后对于subquery也使用这样的进行解析。

得到这样的一个粗略的抽象语法树之后，

对所有的table部分进行替换