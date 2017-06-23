---
layout: post
title: "LeetCode_196. Delete Duplicate Emails"
date: 2017-06-20 17:21:06 +0800
description: LeetCode 数据库系列，删除重复的邮件
tags: 
 - LeetCode_DataBase

---
### 196. Delete Duplicate Emails
Write a SQL query to delete all duplicate email entries in a table named Person, keeping only unique emails based on its smallest Id.

>+----+------------------+
| Id | Email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |
+----+------------------+
Id is the primary key column for this table.

For example, after running your query, the above `Person` table should have the following rows:

>+----+------------------+
| Id | Email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
+----+------------------+

---
---

解答：删除重复的邮箱，按照示例是删除ID较大的重复邮箱：
- 子查询，难点在于构造需要删除的ID的集合：
{%highlight ruby%}
# Write your MySQL query statement below
DELETE FROM person WHERE Id NOT IN(SELECT * FROM (SELECT MIN(Id) FROM person GROUP BY Email) AS P);
{%endhighlight%}

这个写法如果不把查询出的最小ID集合作为`P`的话，会报错：
>You can't specify target table <tbl> for update in FROM clause

意思说，不可以将同一个表中`SELECT`出的数据，再在表上进行删除等更新操作。
- 第二种方式，就是使用连表删除：
{% highlight ruby %}
  DELETE p1 FROM Person p1, Person p2 WHERE p1.Email = p2.Email ANDp1.Id > p2.Id;
{% endhighlight %}