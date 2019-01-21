---
layout: post
title:  "sed常用命令记录"
date:   2019-01-21 20:00:00
categories: Linux
tags: Linux, sed
author: LuckyBoy
location: Beijing, China
description: sed常用的一些命令记录
---
---

# 文件处理类

## 1. 定址

```bash
sed -n '3p' datafile   # 打印第三行
sed -n '100, 300p' datafile  # 打印100到300行
sed '/My/,/You/d' datafile  # 删除包含"My"的行到包含"You"的行之间的行
sed '/My/,10d' datafile  # 删除包含"My"的行到第十行的内容
```

## 2. 命令

### 1) p命令

显示模式空间的内容

### 2) d命令

删除输入行，显示剩余的数据

```bash
sed '/my/d' datafile
# 删除包含my的行，其余的都被显示
```

### 3) s命令

```bash
sed 's/^My/You/g' datafile
#命令末端的g表示在行内进行全局替换，也就是说如果某行出现多个My，所有的My都被替换为You。

sed -n '1,20s/My$/You/gp' datafile
#取消默认输出，处理1到20行里匹配以My结尾的行，把行内所有的My替换为You，并打印到屏幕上

sed -i 's/Old/New' My_File.txt
# mac中需要添加 -ig才能够执行
```

未完待续。。。