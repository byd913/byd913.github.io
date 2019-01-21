---
layout: post
title:  "centos修改GLIBC版本"
date:   2019-01-21 16:00:00
categories: Linux
tags: Linux, centos, glibc
author: LuckyBoy
location: Beijing, China
description: 修改centos系统glibc的默认版本号
---
---

# 一. 支持glibc版本的查看

```bash
strings /lib64/libc.so.6 |grep GLIBC_
```

# 二. 修改glibc版本

查看libc.so.6软链的信息

```bash
ll -h libc.so.6
```

删除软链

```bash
rm libc.so.6
```

在删除`libc.so.6`之后，所有的命令由于基本都依赖于`libc.so.6`，所以如ls, ln等命令都不能使用。因此我们需要使用到LD_PRELOAD变量

```bash
LD_PRELOAD=/lib64/libc-2.12.so ln -s /lib64/libc-2.12.so /lib64/libc.so.6
```

至此，glibc的版本已经更新成功