---
layout: post
title:  "python pip更新源"
date:   2020-08-20 15:00:00
categories: python, pip
tags: python, pip
author: LuckyBoy
location: Beijing, China
description: python导出项目依赖的包
---
---


## 一、更新pip使用的源

我们在使用pip按照依赖包的时候，默认使用的是pypi的源，但是访问pypi的速度相对国内的源比较慢，在安装一些比较大的包的时候就很恼火。
在国内也有一些pypi的源，具体如下:
* 豆瓣 http://pypi.douban.com/
* 华中理工大学 http://pypi.hustunique.com/
* 山东理工大学 http://pypi.sdutlinux.org
* 中国科学技术大学 http://pypi.mirrors.ustc.edu.cn

在安装的时候，我们可以使用pip的`-i`参数手动指定更新源，例如
```
pip -i http://pypi.douban.com/ install Flask
```

如果每次都这样指定的话，就非常的麻烦。可以配置当前用户使用的pip源。
1. 在当前用户的家目录新建`.pip`文件夹
```
cd ~ && mkdir .pip
```
2. 在`.pip`目录下创建`pip.conf`文件并填入以下内容(以豆瓣为例)
```
[global]
trusted-host =  pypi.douban.com
index-url = http://pypi.douban.com/simple
```


## 二、导出项目依赖的包
我们开发的python项目正常会依赖一些其它的三方包，为了方便在新的机器上部署运行项目，我们需要将我们使用到的三方依赖包的名称和版本导出。
pip提供了`freeze`命令可以导出当前环境三方包的名称和版本。
```
pip freeze > requirements.txt
```
导出的文件长这样：
```
mqp==2.4.2
aniso8601==3.0.2
asn1crypto==0.24.0
backports-abc==0.5
backports.functools-lru-cache==1.5
backports.shutil-get-terminal-size==1.0.0
billiard==3.5.0.5
bleach==3.0.2
celery==4.2.2
certifi==2018.8.24
cffi==1.11.5
chardet==3.0.4
click==6.7
...
```
在新的机器部署安装三方包的时候，直接使用`-r`参数即可。
```
pip install -r requirements.txt
```
 
但是当我们的开发环境不仅包含项目A依赖包，可能还会包含项目B的依赖包等，使用`pip freeze` 会把所有的依赖包都导出来，
这样我们的`requirements`会非常庞大，怎么能够只导出当前项目使用的依赖包呢？
这时候我们就需要使用`pipreqs`，`pipreqs`会扫描指定的目录，帮助我们生成指定目前使用的依赖包。

首先我们需要先安装`pipreqs`
```
pip install pipreqs
```
然后在我们的项目里面使用以下命令:
```
pipreqs .
```
就会自动生成一个`requirements.txt`文件，这个文件里面就只会包含该项目使用了的三方包名称和版本。
