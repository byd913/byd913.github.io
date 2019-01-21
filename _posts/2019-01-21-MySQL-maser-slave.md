---
layout: post
title:  "MySQL主从同步失败后处理方法"
date:   2019-01-21 18:00:00
categories: MySQL
tags: MySQL, Master, Slave
author: LuckyBoy
location: Beijing, China
description: MySQL在主从同步失败后恢复处理方法
---
---

# 一、背景描述

在MySQL存在主库和从库后，有时候由于一些错误的操作，导致一些语句在从库无法执行，自此从库就会停止在该位置，不再与主库同步。

# 二、错误查看

在MySQL的slave端，可以通过`show slave status\G`查看当前slave的状态。可以主要看以下几个参数:

| 参数名                | 含义                          |
|:----------------------|:------------------------------|
| Slave_IO_Running      | slave与master的IO通信是否正常 |
| Slave_SQL_Running     | slave执行SQL语句是否章程      |
| Last_Errno            | 上次执行MySQL语句的错误码     |
| Last_Error            | 上次执行MySQL语句的错误信息   |
| Seconds_Behind_Master | 当前slave落后master的时间     |

# 三、错误修复

在MySQL的slave端执行以下的命令:

```sql
-- 1. 暂停slave
stop slave

-- 2. 设置slave忽略的事件数目
set global sql_slave_skip_counter=1;

-- 3. 重新打开slave
start slave
```