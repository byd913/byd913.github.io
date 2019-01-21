---
layout: post
title:  "tmux常用快捷键"
date:   2019-01-21 14:00:00
categories: Python
tags: Python, Jupyter, Convert
author: LuckyBoy
location: Beijing, China
description: jupyter文件格式(ipynb)转换为其他格式文件
---
---

# 背景说明

我们在用jupyter写完代码或者文档后，如果要在其它的地方使用，通常需要转换为其他的格式。

# ipynb文件转py files

```bash
jupyter nbconvert --to script notebook.ipynb
```

# 其他可以输出格式

## html

```--to html```

## latex

```--to latex```

## markdown

```--to markdown```

## pdf

```--to pdf```