---
layout: post
title:  "Boost Ptree库多线程解析JSON崩溃"
date:   2018-05-10 11:05:00
categories: Boost
tags: Boost, Ptree, JSON
author: LuckyBoy
location: Beijing, China
description: 解决Boost PTree多线程解析JSON崩溃问题
---
---

boost ptree做解析的时候使用的是**spirit**，这个库默认是**非线程安全**的。
如果要在多线程下使用，需要在头文件include前，定义语法解析库线程安全宏**BOOST_SPIRIT_THREADSAFE**。

```cpp
#define BOOST_SPIRIT_THREADSAFE
#include <boost/spirit.hpp>
```

```cpp
#define BOOST_SPIRIT_THREADSAFE 
#include <boost/property_tree/ptree.hpp>
#include <boost/property_tree/json_parser.hpp> 
```
