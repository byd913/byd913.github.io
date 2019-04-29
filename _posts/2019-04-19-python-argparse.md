---
layout: post
title:  "Python使用argparse解析命令行参数"
date:   2019-04-19 10:00:00
categories: Python
tags: Python, argparse
author: LuckyBoy
location: Beijing, China
description: 使用argparse模块解析Python的命令参数和构建脚本帮助说明信息
---
---

# 一、背景
博主之前在处理python脚本命令行参数的时候，都是自己从sys.argv里面取读取list数据，然后规定第几个代表啥含义。这样在参数比较少的时候，还基本可以满足，但是当命令行参数比较多（5个或者更多）的时候，整体的参数就会比较混乱。

Python模块自带了一个命令行参数解析的模块（argparse）。 argparse会根据配置自动增加`-h`帮助参数，给出配置参数说明信息，接下来我们会用具体例子说明。

# 二、常用函数介绍

## ArgumentParser
ArgumentParser会生成一个参数的解析器，它主要有以下参数：
```
- prog -- The name of the program (default: sys.argv[0])
- usage -- A usage message (default: auto-generated from arguments)
- description -- A description of what the program does
```

## add_argument
add_argument会增加一个命令行的参数，使用的示例如下：
```python
parser.add_argument('-n', '--batch-number', help='batch number for task', required=True)
```

## parse_args
parse_args会解析输入的命令行参数，然后返回解析的结果。


# 三、使用示例
我们编写如下的python脚本

```python
# -*- coding=utf-8 -*-
import argparse


if __name__ == '__main__':
    parser = argparse.ArgumentParser()
    parser.add_argument('-n', '--batch-number',
                        help='batch number for task', required=True)
    parser.add_argument('-st', '--start-time',
                        help='collection start time, format as 2018-10-12', required=True)
    parser.add_argument(
        '-et', '--end-time', help='collection end time, format as 2018-10-12', required=True)
    parser.add_argument('-d', '--distinct',
                        help='if deduplicate data on same link', default=0)

    cmd_result = parser.parse_args()

    print cmd_result.batch_number
    print cmd_result.start_time
    print cmd_result.end_time
    print cmd_result.distinct
```

如果我们不加任何参数，直接运行脚本`python xxx.py`，则会收到以下的提示：
```
usage: test.py [-h] -n BATCH_NUMBER -st START_TIME -et END_TIME [-d DISTINCT]
test.py: error: argument -n/--batch-number is required
```
我们使用`-h`参数，获取帮助信息，会得到以下的提示：
```
usage: test.py [-h] -n BATCH_NUMBER -st START_TIME -et END_TIME [-d DISTINCT]
optional arguments: 
  -h, --help            show this help message and exit
  -n BATCH_NUMBER, --batch-number BATCH_NUMBER      
                        batch number for task   
  -st START_TIME, --start-time START_TIME     
                        collection start time, format as 2018-10-12
  -et END_TIME, --end-time END_TIME
                        collection end time, format as 2018-10-12
  -d DISTINCT, --distinct DISTINCT
                        if deduplicate data on same link
```
