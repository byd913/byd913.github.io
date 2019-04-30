---
layout: post
title:  "git配置多个用户使用"
date:   2019-04-29 15:00:00
categories: git, Linux
tags: git, user, ssh
author: LuckyBoy
location: Beijing, China
description: 配置在同一个Linux用户下面，多个git用户同时使用提交
---
---

## 一、背景

在多人同时开发的时候，经常遇到一台Linux开发机多人同时使用且都使用同一个Linux用户。多个人都需要提交git，怎么能够指定git提交的时候使用自己ssh key呢？

下面举例说明如何配置，假如我们有A和B两个用户，都在同一个Linux用户`user`目录下面开发，都需要使用git提交。


## 二、ssh配置

首先我们使用`ssh-keygen`生成自己的私钥和公钥。

```shell
ssh-keygen

# 填写自己的密钥名称
enerating public/private rsa key pair.
Enter file in which to save the key (/home/user/.ssh/id_rsa): /home/user/.ssh/id_rsa_a
# 后面一路回车键结束
```

然后我们在`.ssh`目录下面新建一个`config`文件，修改`config`文件的权限为`644`

```shell
chmod 644 config
```

在文件中填入以下的内容

```shell
host git_a
    User git
    Port 22
    HostName git.github.com
    IdentityFile ~/.ssh/id_rsa_a
```

上面的`gitlab`为一个别名，HostName填写对应git远端仓库的Host地址，IdentityFile填写刚才生成的密钥文件。
致辞，ssh相关的配置就完成了，当然还需要将`~/.ssh/id_rsa_a.pub`里面的内容添加到你Git的`SSH Keys`里面。


## 三、工程的git配置修改

接下来到你的工程目录下面，在`.git`目录下面找到`config`文件，可以看到里面有以下类似的内容:

```shell
[remote "origin"]
    url = git@xxxxxx:a/xxx.git
    fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
    remote = origin
    merge = refs/heads/master
```
修改其中的`url = git@xxxxxx:a/xxx.git`为`url = git@git_a:a/xxx.git`,也就是指定了当前工程git使用`git_a`里面的配置做处理。
后面改工程目录的pull或push都是使用`git_a`的配置处理。
