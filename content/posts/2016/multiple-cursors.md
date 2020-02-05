---
layout: post
title:  "multiple cursors"
date:   2016-09-21 09:51:02
categories: multiple cursor sublime emacs
---

## multiple cursor in emacs

### install
先用M-x输入package-install 安装multiple-cursors包
[Multiple Cursors](https://github.com/magnars/multiple-cursors.el)

### config
在配置文件中开启`multiple-cursors`：

```clojure
(require 'multiple-cursors)
(global-set-key (kbd "C-S-c C-S-c") 'mc/edit-lines)

(global-set-key (kbd "C->") 'mc/mark-next-like-this)
(global-set-key (kbd "C-<") 'mc/mark-previous-like-this)
(global-set-key (kbd "C-c C-<") 'mc/mark-all-like-this)

(defalias 'mc-mode 'multiple-cursors-mode)
```

### useage
M-x后输入mc-mode

如果开启了[evil](https://www.douban.com/group/topic/34775654/)
最好先按i进入普通模式

然后使用C-c C-<全选中后，就可以随意编排了




PS: command+k 在Mac命令行里好爽
