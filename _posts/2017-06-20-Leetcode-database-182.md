---
layout: post
title: "LeetCode_182. Duplicate Emails"
date: 2017-06-20 14:21:06 +0800
description: LeetCode 数据库系列，输出重复邮件
tags: 
 - LeetCode_DataBase

---
### 182. Duplicate Emails
Write a SQL query to find all duplicate emails in a table named Person.
>+----+---------+
| Id | Email   |
+----+---------+
| 1  | a@b.com |
| 2  | c@d.com |
| 3  | a@b.com |
+----+---------+

For example, your query should return the following for the above table:

>+---------+
| Email   |
+---------+
| a@b.com |
+---------+

Note: All emails are in lowercase.

---
---
解答：找出数据中重复的邮件，依然给出两种实现方式：
- 直接查询，分组看个数是否大于1：
{%highlight ruby%}
SELECT Email FROM Person GROUP BY Email HAVING COUNT(Email) > 1;
{%endhighlight%}

- 联表查询：
{%highlight ruby%}
SELECT DISTINCT p1.Email FROM Person p1,Person p2 WHERE p1.Email=p2.Email AND p1.Id!=p2.Id;
{%endhighlight%}