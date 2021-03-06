---
title: MySQL存储引擎那些事
date: 2021-02-04 17:14:39
description:
tags: [编程, 过去]
category:
    - 100 学习类
    - 110 编程
    - 113 数据库
---

## 背景

真是造化弄人。

一开始是想看mysql的主从配置，后来因为主从同步出错的关系看了一下mysql的日志体系，然后突然想起mysql的引擎，遂再学习一下。初步打算学习完引擎后便对msql暂放一段落，再踏入新征程，岂不正如人生，来来回回那些事，不过是循环往复，其中更有变化多端，且记，再进一步，便有进一步的欢喜！

## Mysql中常用的四种存储引擎

MySQL中常用的四种存储引擎分别是： MyISAM存储引擎、innoDB存储引擎、MEMORY存储引擎、ARCHIVE存储引擎。本文将对这四种存储引擎作出重点介绍，最后对这四种存储引擎进行比较。

### 存储引擎

1、存储引擎其实就是对于数据库文件的一种存取机制，如何实现存储数据，如何为存储的数据建立索引以及如何更新，查询数据等技术实现的方法。

2、MySQL中的数据用各种不同的技术存储在文件（或内存）中，这些技术中的每一种技术都使用不同的存储机制，索引技巧，锁定水平并且最终提供广泛的不同功能和能力。在MySQL中将这些不同的技术及配套的相关功能称为存储引擎。

### MySQL中查看引擎

1、show engines; // 查看mysql所支持的存储引擎，以及从中得到mysql默认的存储引擎。

2、show variables like '% storage_engine'; // 查看mysql 默认的存储引擎

3、show create table tablename ; // 查看具体某一个表所使用的存储引擎，这个默认存储引擎被修改了！

4、show table status from database where name="tablename" //准确查看某个数据库中的某一表所使用的存储引擎

5、ALTER TABLE 待改表名 engine=innodb;//修改已建成表的引擎

6、设置InnoDB为默认引擎：

vi  /etc/my.cnf

在[mysqld] 下面加入

default-storage-engine=InnoDB

保存后重新启动mysql

### MySQL中常用的几种存储引擎

#### InnoDB存储引擎（推荐）

InnoDB是事务型数据库的首选引擎，支持事务安全表（ACID），支持行锁定和外键，InnoDB是默认的MySQL引擎。

> InnoDB主要特性

- 为MySQL提供了具有提交、回滚和崩溃恢复能力的事物安全（ACID兼容）存储引擎。InnoDB锁定在行级并且也在`SELECT`语句中提供一个类似Oracle的非锁定读。这些功能增加了多用户部署和性能。在SQL查询中，可以自由地将InnoDB类型的表和其他MySQL的表类型混合起来，甚至在同一个查询中也可以混合
- InnoDB存储引擎为在主内存中缓存数据和索引而维持它自己的缓冲池。InnoDB将它的表和索引在一个逻辑表空间中，表空间可以包含数个文件（或原始磁盘文件）。这与MyISAM表不同，比如在MyISAM表中每个表被存放在分离的文件中。InnoDB表可以是任何尺寸，即使在文件尺寸被限制为2GB的操作系统上
- InnoDB支持外键完整性约束，存储表中的数据时，每张表的存储都按主键顺序存放，如果没有显示在表定义时指定主键，InnoDB会为每一行生成一个6字节的ROWID，并以此作为主键
- InnoDB存储引擎最重要的是支持事务，以及事务相关联功能
- InnoDB存储引擎索引使用的是B+Tree
- InnoDB支持自增长列（auto_increment）,自增长列的值不能为空，如果在使用的时候为空的话怎会进行自动存现有的值开始增值，如果有但是比现在的还大，则就保存这个值。

使用 **InnoDB存储引擎** MySQL将在数据目录下创建一个名为 `ibdata1 `的10MB大小的自动扩展数据文件，以及两个名为`ib_logfile0`和`ib_logfile1`的5MB大小的日志文件。数据库文件包括在库下以表名开头的.frm和.ibd文件。

优缺点：InnoDB的优势在于提供了良好的事务处理、崩溃修复能力和并发控制。缺点是读写效率较差，占用的数据空间相对较大。

#### MyISAM存储引擎

MyISAM基于ISAM存储引擎，并对其进行扩展。它是在Web、数据仓储和其他应用环境下最常使用的存储引擎之一。MyISAM拥有较高的插入、查询速度，但不支持事务。

> MyISAM主要特性：

- 被大文件系统和操作系统支持
- 当把删除和更新及插入操作混合使用的时候，动态尺寸的行产生更少碎片。这要通过合并相邻被删除的块，若下一个块被删除，就扩展到下一块自动完成
- 每个MyISAM表最大索引数是64，这可以通过重新编译来改变。每个索引最大的列数是16
- 最大的键长度是1000字节，这也可以通过编译来改变，对于键长度超过250字节的情况，一个超过1024字节的键将被用上
- BLOB和TEXT列可以被索引
- NULL被允许在索引的列中，这个值占每个键的0~1个字节
- 所有数字键值以高字节优先被存储以允许一个更高的索引压缩
- 每个MyISAM类型的表都有一个AUTO_INCREMENT的内部列，当INSERT和UPDATE操作的时候该列被更新，同时AUTO_INCREMENT列将被刷新。所以说，MyISAM类型表的AUTO_INCREMENT列更新比InnoDB类型的AUTO_INCREMENT更快
- 可以把数据文件和索引文件放在不同目录
- 每个字符列可以有不同的字符集
- 有VARCHAR的表可以固定或动态记录长度
- VARCHAR和CHAR列可以多达64KB

使用MyISAM引擎创建数据库，将产生3个文件。文件的名字以表名字开始，扩展名之处文件类型：frm文件存储表定义、数据文件的扩展名为.MYD（MYData）、索引文件的扩展名时.MYI（MYIndex）。

优缺点：MyISAM的优势在于占用空间小，处理速度快。缺点是不支持事务的完整性和并发性。

#### MEMORY存储引擎

memory存储引擎相比前面的一些存储引擎，有点不一样，其使用存储在内从中的数据来创建表，而且所有的数据也都存储在内存中。

每个基于memory存储引擎的表实际对应一个磁盘文件，该文件的文件名和表名是相同的，类型为.frm。该文件只存储表的结构，而其数据文件，都是存储在内存中，这样有利于对数据的快速处理，提高整个表的处理能力。

memory存储引擎默认使用哈希（HASH）索引，其速度比使用B-+Tree型要快，如果读者希望使用B树型，则在创建的时候可以引用。

memory存储引擎文件数据都存储在内存中，如果mysqld进程发生异常，重启或关闭机器这些数据都会消失。所以memory存储引擎中的表的生命周期很短，一般只使用一次。

#### ARCHIVE存储引擎

该存储引擎非常适合存储大量独立的、作为历史记录的数据。区别于InnoDB和MyISAM这两种引擎，ARCHIVE提供了压缩功能，拥有高效的插入速度，但是这种引擎不支持索引，所以查询性能较差一些。

### 四种存储引擎比较

InnoDB：支持事务处理，支持外键，支持崩溃修复能力和并发控制。如果需要对事务的完整性要求比较高（比如银行），要求实现并发控制（比如售票），那选择InnoDB有很大的优势。如果需要频繁的更新、删除操作的数据库，也可以选择InnoDB，因为支持事务的提交（commit）和回滚（rollback）。

MyISAM：插入数据快，空间和内存使用比较低。如果表主要是用于插入新记录和读出记录，那么选择MyISAM能实现处理高效率。如果应用的完整性、并发性要求比 较低，也可以使用。如果数据表主要用来插入和查询记录，则MyISAM引擎能提供较高的处理效率

MEMORY：所有的数据都在内存中，数据的处理速度快，但是安全性不高。如果需要很快的读写速度，对数据的安全性要求较低，可以选择MEMOEY。它对表的大小有要求，不能建立太大的表。所以，这类数据库只使用在相对较小的数据库表。如果只是临时存放数据，数据量不大，并且不需要较高的数据安全性，可以选择将数据保存在内存中的Memory引擎，MySQL中使用该引擎作为临时表，存放查询的中间结果

如果只有INSERT和SELECT操作，可以选择Archive，Archive支持高并发的插入操作，但是本身不是事务安全的。Archive非常适合存储归档数据，如记录日志信息可以使用Archiv

注意，同一个数据库也可以使用多种存储引擎的表。如果一个表要求比较高的事务处理，可以选择InnoDB。这个数据库中可以将查询要求比较高的表选择MyISAM存储。如果该数据库需要一个用于查询的临时表，可以选择MEMORY存储引擎。































