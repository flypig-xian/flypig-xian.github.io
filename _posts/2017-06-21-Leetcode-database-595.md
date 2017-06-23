---
layout: post
title: "LeetCode_595. Big Countries"
date: 2017-06-21 15:21:06 +0800
description: LeetCode 数据库系列，大型国家
tags: 
 - LeetCode_DataBase

---
### 595. Big Countries
There is a table World

>+-----------------+------------+------------+--------------+---------------+
| name            | continent  | area       | population   | gdp           |
+-----------------+------------+------------+--------------+---------------+
| Afghanistan     | Asia       | 652230     | 25500100     | 20343000      |
| Albania         | Europe     | 28748      | 2831741      | 12960000      |
| Algeria         | Africa     | 2381741    | 37100000     | 188681000     |
| Andorra         | Europe     | 468        | 78115        | 3712000       |
| Angola          | Africa     | 1246700    | 20609294     | 100990000     |
+-----------------+------------+------------+--------------+---------------+

A country is big if it has an area of bigger than 3 million square km or a population of more than 25 million.

Write a SQL solution to output big countries' name, population and area.

For example, according to the above table, we should output:

>+--------------+-------------+--------------+
| name         | population  | area         |
+--------------+-------------+--------------+
| Afghanistan  | 25500100    | 652230       |
| Algeria      | 37100000    | 2381741      |
+--------------+-------------+--------------+

---
---

解答：非常简单，没啥说的，一次搞定：
{%highlight ruby%}
# Write your MySQL query statement below
SELECT name,population,area FROM world WHERE area > 3000000 OR population > 25000000
{%endhighlight%}