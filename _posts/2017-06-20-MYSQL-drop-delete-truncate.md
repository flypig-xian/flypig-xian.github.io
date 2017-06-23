---
layout: post
title: "MYSQL中删除数据表的三种方式"
date: 2017-06-20 14:21:06 +0800
description: MYSQL中的drop and delete and truncate
tags: 
 - LeetCode_DataBase

---
### MYSQL中删除数据表的三种方式
- DROP
使用方式：
> drop table tbl_name;

删除数据表的内容和定义，释放空间。彻底删除表。

- TRUNCATE
使用方式：
> TRUNCATE TABLE tbl_name;
清空数据表，释放空间，保留表结构，表状态信息回复原始状态(自增ID从0开始)。

- DELETE
使用方式：
>DELETE TABLE tbl_name;

  逐行删除表数据，会触发事务，删除可通过`ROLLBACK`撤销。
空间不回收，可以通过 
> OPTIMIZE TABLE  tbl_name;

  优化表空间。