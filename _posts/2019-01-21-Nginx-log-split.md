---
layout: post
title:  "Nginx日志切分和清理"
date:   2019-01-21 08:00:00
categories: Nginx
tags: Nginx, Log split, crontab
author: LuckyBoy
location: Beijing, China
description: 定时切分和清理Nginx日志
---
---

# 背景

nginx产生的日志自动切分，长时间的日志积累会导致超大的日志文件，不便于日志的分析和清理。
因此我们需要对nginx的日志进行定时的切分（每天或每周）。

# 日志的切分

nginx实现了对`USR1`信号的处理，在接收到`USR1`后，Nginx会重新打开日志文件。
因此我们先将日志文件rename，然后在给Nginx发送USR1信号就可以实现日志的切分。
具体实现如下：

```bash
# /bin/bash

logs_path=/home/user/nginx/logs/
pid_file=/home/user/nginx/logs/nginx.pid

error_log_name=error.log
web_service_log_name=web_service.access.log

date_suffix=`date -d '-1 day' '+%Y-%m-%d'`

mv ${logs_path}${error_log_name} ${logs_path}${error_log_name}'.'${date_suffix}
mv ${logs_path}${web_service_log_name} ${logs_path}${web_service_log_name}'.'${date_suffix}

kill -USR1 `cat ${pid_file}`
```

# 日志的清理

```shell
# /bin/bash

logs_path=/home/user/nginx/logs/
pid_file=/home/user/nginx/logs/nginx.pid

error_log_name=error.log

cd ${logs_path}
find . -mtime +60 -name ${error_log_name}'.*' | xargs rm -f
```

# 定时执行

将上面的脚本保存为文件，然后在`crontab`中添加任务(*crontab -e*)。

```shell
# 每天00:00执行切分
0 0 * * * cd /home/user/nginx/script && sh nginx_log_rotate.sh &

# 每周一早上00:00执行切分
0 0 * * 1 cd /home/user/nginx/script && sh nginx_log_rotate.sh &
```