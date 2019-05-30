---
layout: post
title:  "mysql的4种事务级别"
date:   2019-05-28 18:00:00
categories: mysql, Linux
tags: mysql, transaction
author: LuckyBoy
location: Beijing, China
description: mysql有四个事务: READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ和SERIALIABLE; 不同级别在效率和事务的隔离性上表现有所不同。
---
---


在SQL标准中定义了4种事务隔离级别，每种隔离级别规定了在当前事务所做的修改，是否在事务内和事务间可见，下面分别介绍下四种隔离级别。

## READ UNCOMMITTED

READ UNCOMMITTED级别规定，在当前事务所做的修改，即使没有commit，在其他的事务也是可见的。

这样容易造成脏读(Dirty Read)，因为事务的所有修改都有可能被rollback，读取到被rollback的数据也就成了脏数据。


## READ COMMITTED

READ COMMITTED级别规定，在事务内所做的修改，在commit之前，只对事务内可见，对于其他事务不可见。只有在事务commit之后，其他事务才可见。

这样没有了脏读的问题，但是不可重复读(UNREPEATED READ)问题依然存在，即一个事务在另一个事务commit前后同样的查询得到的结果可能不一致。


## REPEATABLE READ

REPEATABLE READ级别规定，一个事务多次查询同一个数据的结果始终是一致的，这样解决了不可重复读问题，但是还是无法解决另外一个幻读(Phantom read)问题。

幻读是指某个事务读取某个范围内的数据后，其他的事务在改范围内插入了数据，该事务再次读取该范围的数据的时候，会产生幻行(Phantom Row)。

Innodb和XtraDB存储引擎通过多版本并发控制(MVCC)解决了幻读的问题。

REPEATABLE READ 是MySQL默认的事务隔离级别。


## SERIALIABLE 

SERIALIABLE是最高的事务隔离级别，它通过强制的事务串行执行，解决了前面的幻读问题。
它在事务读取每行数据的时候，都会加锁，从而会有大量的锁竞争问题，实际情况下很少使用该事务级别。


## 总结

| 隔离级别         | 脏读 | 不可重复读 | 幻读 | 加锁读 |
|------------------+------+------------+------+--------|
| READ UNCOMMITTED | Y    | Y          | Y    | N      |
| READ COMMITTED   | N    | Y          | Y    | N      |
| REPEATABLE READ  | N    | N          | Y    | N      |
| SERIALIABLE      | N    | N          | N    | Y      |


## 事务隔离级别查看和设置

在MySQL中可以通过以下语句查看当前的隔离级别

```mysql
    select @@tx_isolation;
```

在MySQL中可以通过以下的语句设置当前session的事务隔离级别

```mysql
    set session transaction isolation level {level}
```

level可以有以下的取值
* read uncommited: 可以读取未commit的数据
* read commited: 只能读取已经commit的数据 -- oracle默认级别
* repeated read: 可以重复读 -- mysql默认级别
* serializable: 串行化 -- 相当于锁表
