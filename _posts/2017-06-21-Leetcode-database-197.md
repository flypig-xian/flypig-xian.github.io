---
layout: post
title: "LeetCode_197. Rising Temperature"
date: 2017-06-21 10:21:06 +0800
description: LeetCode 数据库系列，温度上升
tags: 
 - LeetCode_DataBase

---
### 197. Rising Temperature
Given a Weather table, write a SQL query to find all dates' Ids with higher temperature compared to its previous (yesterday's) dates.

>+---------+------------+------------------+
| Id(INT) | Date(DATE) | Temperature(INT) |
+---------+------------+------------------+
|       1 | 2015-01-01 |               10 |
|       2 | 2015-01-02 |               25 |
|       3 | 2015-01-03 |               20 |
|       4 | 2015-01-04 |               30 |
+---------+------------+------------------+

For example, return the following Ids for the above Weather table:

>+----+
| Id |
+----+
|  2 |
|  4 |
+----+

---
---

解答：找出温度升高那天的Id，题目比较简单，关键是如何找出连续的两天,需要借助MySQL内置的天数转换函数(DATADIFF/TODAYS)：
{%highlight ruby%}
# Write your MySQL query statement below
SELECT W1.Id FROM Weather AS W1, Weather AS W2
WHERE W1.Temperature > W2.Temperature AND DATEDIFF(W1.Date, W2.Date) = 1;
{%endhighlight%}