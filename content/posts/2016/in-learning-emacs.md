---
layout: post
title:  "in learning emacs"
date:   2016-08-17 09:51:02
categories: learning emacs
---

## 之前的失败经历

曾经尝试了两次，都以失败告终。
第一次是教程不咋地，没教什么好东西
第二次无教程尝试spacemacs，虽然vi模式可以方便编辑，但是保存之类的不是很好使，
放弃。

## 再次尝试

[安装](http://clojure-doc.org/articles/tutorials/emacs.html)
基本上依靠brew，可以解决大部分问题

用clojure也快两年了，最近又想折腾下nREPL，
就再尝试学习一下emacs，提升一下这方面的技能。
[基础emacs](http://www.braveclojure.com/basic-emacs/)
PS：注意，最新的cider-nrepl早就不是0.8.1了，表被坑，可以上[这里](https://clojars.org/cider/cider-nrepl)查看

本来还打算用vi模式来进行学习，不过怎么想，学回来的应该都是半吊子。
所以还不如之间学习emacs的操作方式比较好。

参考[这里](http://stackoverflow.com/questions/14905133/how-to-set-cmd-key-binding-in-emacs)将mac的comand设置成emacs中的control了



## 连接docker内的nREPL
参考这里
[StackOverflow](http://stackoverflow.com/questions/22422820/connecting-to-a-headless-nrepl-running-in-a-docker-container-from-another-contai)
所说，可以直接在docker内部启动一个nrepl端口，然后从外部进行连接。另外figwheel本身也有类似说法。


## nREPL in figwheel

[参考](https://github.com/bhauman/lein-figwheel/wiki/Using-the-Figwheel-REPL-within-NRepl)

参照上面的教程，将figwheel的nREPL配置起来

## 神奇的undo和redo

简而言之，undo是在对历史操作进行回朔，
如果你在其中插入任何其他操作，比如C-G（或移动光标）。
那么就会用之前回朔到的状态，创建一个新历史，放在历史的顶端。
这是时候如果再进行undo，就会undo掉回朔历史，创建历史的操作，从而实现redo的效果。

## repl
连上正常的repl之后，执行如下命令：

```clojure
(do (require 'figwheel-sidecar.repl-api)
           (figwheel-sidecar.repl-api/start-figwheel!)
           (figwheel-sidecar.repl-api/cljs-repl))
```
即可加入cljs的repl模式

C-c M-N 切换到当前ns
