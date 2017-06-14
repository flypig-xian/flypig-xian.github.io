---
layout: post
title: "MYSQL_Operations"
date: 2017-06-01 11:41:06 +0800
description: MYSQL，不断完善
tags: 
 - MYSQL
 - DATABASE
---
## 常用指令
### DDL(DATA DEFINITION LANGUAGE):数据定义语言语言
- `CREATE DATABASE [IF NOT EXISTS] db_name
    [DEFAULT] CHARACTOR SET [=] charset_name` 生成数据库；
- `SHOW CREATE DATABASE db_name \G` 显示数据库的构造语句与编码方式；
- `CREATE TABLE [IF NOT EXISTS] tbl_name(create_defination,...)[table_options][partition_options]`　创建数据表
    - create_defination:`(col_name col_defination |primay key (index_col_name) | [constraint [symbol]] [unique|fulltext|spatial] [index|key] [index_name] (index_col_name[length]) [ASC|DESC])|[constraint [symbol]] foreign key [index_name] (index_col_name,...) references tal_name(index_col_name,....))`
    - table_options:`engine [=] engine_name|auto_increment[=] value | [default] charactor set [=] charset_name`
- `SHOW CREATE TABLE tbl_name \G` 显示数据表的构造语句与编码方式；
- `DROP DATABASE [IF EXISTS] db_name` 删除数据库；
- `DROP TABLE [IF EXITSTS] tbl_name` 删除数据表；
- `ALTER TABLE tbl_name ADD [COLUMN] (col_name column_defination,...) [FIRST|AFTER] index_col_name` 修改数据表——增加列；
- `ALTER TABLE tbl_name ADD primay key(index_col_name)` 修改数据表——增加主健；
-  `ALTER TABLE tbl_name ADD [CONSTAINT [symbol]] [unique|fulltext|spatial] [index|key] [index_name] (index_col_name) [ASC|DESC]` 修改在数据表——增加索引；
-  `ALTER TABLE tbl_name MODIFY [column] col_name column_defination [first|after] col_name` 修改数据表——修改字段;
-  `ALTER TABLE tbl_name CHANGE [COLUMN] old_col_name new_col_name column_defination [first|after] col_name` 修改数据表——修改字段（给出字段名）
- `ALTER TABLE tbl_name RENAME [TO|AS] new_tbl_name` 重命名表名；
- `ALTER TABLE tbl_name RENAME [INDEX|KEY] old_index_name TO new_index_name` 重命名索引名称名称；
- `ALTER TABLE tbl_name DROP xxx`
  - `[COLUMN] col_name` 删除列
  - `primary key` 删除主健主键
  - `[index|key] index_name ` 删除索引
  - `foreign key fk_symbol` 删除外键
- `ALTER TABLE tbl_name engine[=]engine_name` 修改表引擎；
### DML(DATA MANIPULATION LANGUAGE)数据操作语言
- `SELECT select_expr [FROM table_references] [WHERE where_condition] [GROUP BY {col_name|expr|position} [ASC|DESC]] [HAVING where_condition] [ORDER BY {col_name|expr|position} [ASC|DESC]] [LIMIT{[off_set],row_count}]` 查询数据
  - PS：having 用在聚合后筛选数据，一般用在group by 之后，而where是聚合前筛选数据。
- `INSERT INTO tbl_name [(col_name1,...)] VALUES (value1,...)` 插入数据
- `UPDATE tbl_references SET col_name1={expr1|DEFAULT} [,col_name2={expr2|DEFAULT}...] [WHERE where_condition] [ORDER BY...] [LIMIT row_count]` 修改数据
- `DELETE FROM TABLE tbl_name [WHERE where_condition] [ORDER BY...][LIMIT row_count]` 删除数据
### TCL(Transaction control language)：事务控制语言
- 事务(Transaction):一个独立的工作单元，一组原子性的SQL查询语句组合。
- MYSQL默认事务自动提交，因此开启事务必须使用`beign | start transaction`或者`set autocommit = 0`
- `commit` 提交事务
- `rollback` 回滚事务