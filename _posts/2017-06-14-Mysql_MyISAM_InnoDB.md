---
layout: post
title: "Myisam与Innodb区别"
date: 2017-06-14 19:11:06 +0800
description: MYSQL经典问题，随时更新
tags: 
 - MYSQL
 - interview
---
关于这个问题，网上的版本很多，但是全面的很少，有的答案很陈旧，特整理后出来，以备自己查询：
1. MyISAM普遍认为有更快查询速度，但是最新的Mysql中InnoDB的大幅改进，两者速度基本没有差别。
2. MyISAM支持`FULLTEXT`全文索引，而InnonDB从5.6开始也支持全文索引，因此，这一项不同也不在存在。
3. InnoDB支持外键/事务/行锁；
4. InnoDB中一定会有主健，索引也会包含主健(覆盖索引)；
5. MyISAM中保存了行数，在`SELECT COUNT(*) FROM tbl_name`中速度会更快。
6. MyISAM中索引与数据分开存储（非聚集索引），InnoDB中数据和索引是一起存储的。MyISAM中索引数据保存的数据地址(指针)，而InnoDB索引是数据本身(聚集索引)，其次，InnoDB的辅助索引中保存的是相应的主健的值，因此辅助索引检测需要两遍索引：首先检测辅助索引获得主健，随后用主健到主索引中检索获得相应记录。
7. InnoDB支持热备份，安全恢复。

