---
layout: post
title:  "设置ssh免密登录"
date:   2019-01-21 12:00:00
categories: Linux
tags: Linux, ssh, Login
author: LuckyBoy
location: Beijing, China
description: 在机器间使用ssh免密登录
---
---

# 背景描述

在日常的工作中，经常需要在不同的服务器之间切换，每次都输入密码，则会非常麻烦。假如我们有服务器`A`和服务器`B`，我们需要从`A`免密登录到`B`。

# 机器A处理

```bash
 ssh-keygen
```

然后一路回车，回车完后。默认会在用户的home目录下生成一个.ssh文件夹。
目录下有以下两个文件

```bash
id_rsa  id_rsa.pub
```

# 机器B的处理

将机器A刚才生成的id_rsa.pub文件传到机器B，可以通过scp或者HTTP等方式传输。
在用户的home目录下新建一个.ssh目录，如果目录已经存在则跳过这一步.

```bash
mkdir .ssh
```

改变文件夹的权限为700

```bash
chmod 700 .ssh
```

将刚才的id_rsa.pub写到authorized_keys里面

```bash
cat id_rsa.pub >> .ssh/authorized_keys
```

改为authorized_keys权限为600

```bash
chmod 600 .ssh/authorized_keys
```

完成以上步骤后就可以从机器A免密登录到机器B了。
一般大家在操作完成后容易忽略两点，机器A要免密登录到机器B，文件必须有以下的权限要求

1. .ssh 文件夹的权限为`700`
2. authorized_keys文件的权限为`600`
