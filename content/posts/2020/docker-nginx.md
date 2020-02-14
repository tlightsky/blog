---
title: "Docker Nginx"
date: 2020-02-14T18:09:00+08:00
draft: false
---

```yaml
web:
  image: nginx
  volumes:
    - ./www:/usr/share/nginx/html:ro
  ports:
    - 80:80
```