---
layout: post
title: "LeetCode_175 Combine Two Tables"
date: 2017-06-20 10:11:06 +0800
description: LeetCode 数据库系列，合并两张表
tags: 
 - LeetCode_DataBase

---
###  175. Combine Two Tables
Table:`Person`
> +-------------+---------+
| Column Name | Type    |
+-------------+---------+
| PersonId    | int     |
| FirstName   | varchar |
| LastName    | varchar |
+-------------+---------+
PersonId is the primary key column for this table.

Table:`Address`
>+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| AddressId   | int     |
| PersonId    | int     |
| City        | varchar |
| State       | varchar |
+-------------+---------+
AddressId is the primary key column for this table.

Write a SQL query for a report that provides the following information for each person in the Person table, `regardless if there is an address for each of those people:`
>FirstName, LastName, City, State

---
---
解答：很简单的一道题目，就是一个联表查询，但是第一次提交错误，原因是没有注意红色字的部分，对于`Person`表中的数据，是可以没有地址的，所以要改用左联查询。

{% highlight php %}
# Write your MySQL query statement below
SELECT FirstName, LastName, City, State FROM Person LEFT JOIN Address ON  Person.PersonId=Address.PersonId
{% endhighlight%}

也可以用`USING`字段，可以用如下查询语句:
{% highlight php %}
# Write your MySQL query statement below
SELECT FirstName, LastName, City, State FROM Person LEFT JOIN Address USING(PersonId)
{% endhighlight%}