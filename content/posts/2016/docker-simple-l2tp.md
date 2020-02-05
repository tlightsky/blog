---
layout: post
title:  "docker simple l2tp"
date:   2016-07-28 09:51:02
categories: docker l2tp
---

## l2tp in docker


```yaml
l2tp:
  image: siomiz/softethervpn
  ports:
   - "500:500/udp"
   - "4500:4500/udp"
   - "1701:1701/tcp"
  environment:
   - PSK=my-pre-shared-key
   - USERS=my-username:my-password
  cap_add:
  - NET_ADMIN
  restart: always
```