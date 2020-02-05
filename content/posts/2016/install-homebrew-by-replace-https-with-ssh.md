---
layout: post
title:  "github的origin自动从https替换为ssh"
date:   2016-07-30 09:51:02
categories: git https ssh
---

## homebrew 下载https出错

根据[github上的issue](https://github.com/Homebrew/legacy-homebrew/issues/34363)
描述，只需修改`~/.gitconfig`，添加以下内容


```
[url "git@github.com:"]
    insteadOf = "https://github.com/"
```
如果你的git@github.com也不ok的话，请参考：[github socks5 proxy](http://tlightsky.github.io/github/socke5/proxy/2016/07/25/github-socks5-proxy.html)
