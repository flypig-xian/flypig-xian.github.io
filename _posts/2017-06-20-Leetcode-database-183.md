---
layout: post
title: "LeetCode_183. Customers Who Never Order"
date: 2017-06-20 15:21:06 +0800
description: LeetCode 数据库系列，输出不买货的顾客
tags: 
 - LeetCode_DataBase

---
### 183. Customers Who Never Order
Suppose that a website contains two tables, the Customers table and the Orders table. Write a SQL query to find all customers who never order anything.

Table: `Customers.`
>+----+-------+
| Id | Name  |
+----+-------+
| 1  | Joe   |
| 2  | Henry |
| 3  | Sam   |
| 4  | Max   |
+----+-------+

Table: `Orders`.

>+----+------------+
| Id | CustomerId |
+----+------------+
| 1  | 3          |
| 2  | 1          |
+----+------------+

Using the above tables as example, return the following:
>+-----------+
| Customers |
+-----------+
| Henry     |
| Max       |
+-----------+

---
---

解答：找出数据中没有下过订单的顾客：
- 子查询：
{%highlight ruby%}
# Write your MySQL query statement below
SELECT Name AS Customers  FROM customers WHERE id NOT IN(SELECT customerId FROM orders);
{%endhighlight%}

- 联表查询：
{%highlight ruby%}
SELECT c1.Name AS Customers FROM Customers c1 LEFT JOIN Orders b on c1.Id = b.CustomerId WHERE b.CustomerId is null;
{%endhighlight%}