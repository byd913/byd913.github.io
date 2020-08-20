---
layout: post
title:  "使用Python搭建HTTP代理服务"
date:  2019-07-29 15:05:14 +0100
categories: Python
tags: http proxy, python
cover: ""
location: Beijing, China
description: 利用Python搭建HTTP的代理服务
---
---

```python
from twisted.web import proxy, http
from twisted.internet import reactor
from twisted.python import log
import sys
log.startLogging(sys.stdout)


class ProxyFactory(http.HTTPFactory):
    protocol = proxy.Proxy


reactor.listenTCP(8077, ProxyFactory())
    reactor.run()
```
