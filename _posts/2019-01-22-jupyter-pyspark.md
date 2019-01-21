---
layout: post
title: "配置spark为jupyter"
date: 2019-01-22 10:00:00
categories: Spark
tags: Spark, PySpark, Jupyter
author: LuckyBoy
location: Beijing, China
description: tmux常用快捷键记录
---
---

# 背景描述

在使用python编写pyspark代码的时候，能够在jupyter notebook交互执行是非常方便的。

# 一、设置PYSPARK变量

```shell
export PYSPARK_DRIVER_PYTHON=jupyter
export PYSPARK_DRIVER_PYTHON_OPTS='notebook'
```

# 二、 启动pyspark

```shell
pyspark --master=local[*]
```

可以看到启动的是一个jupyter notebook服务，并不是默认python shell了
![启动示例图](https://github.com/byd913/shared_images/blob/master/pyspark_jupyter.png?raw=true)