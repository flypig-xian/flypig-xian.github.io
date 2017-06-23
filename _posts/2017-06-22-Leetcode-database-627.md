---
layout: post
title: "LeetCode_627. Swap Salary"
date: 2017-06-22 15:21:06 +0800
description: LeetCode 数据库系列，交换薪水
tags: 
 - LeetCode_DataBase

---
### 627. Swap Salary
Given a table salary, such as the one below, that has m=male and f=female values. Swap all f and m values (i.e., change all f values to m and vice versa) with a single update query and no intermediate temp table.

For example:

>| id 　| name 　| sex　 | salary |
|----|------|-----|--------|
| 1  | A    | m   | 2500   |
| 2  | B    | f   | 1500   |
| 3  | C    | m   | 5500   |
| 4  | D    | f   | 500    |

After running your query, the above salary table should have the following rows:

>| id　 | name　 | sex 　| salary 　|
|----|------|-----|--------|
| 1  | A    | f   | 2500   |
| 2  | B    | m   | 1500   |
| 3  | C    | f   | 5500   |
| 4  | D    | m   | 500    |

---
---

解答：题目是交换薪水，实际是反转性别，通用方法需要一点点判断：
{%highlight ruby%}
UPDATE salary set sex = CASE sex WHEN 'm' then 'f' else 'm' end;
{%endhighlight%}
或者写成Case搜索函数的形式：
{%highlight ruby%}
UPDATE salary set sex = CASE WHEN sex = 'm' then 'f' else 'm' end;
{%endhighlight%}

MARK一下leetCode网友的两条超短语句：
{%highlight ruby%}
UPDATE salary set sex = IF(sex='m','f','m');
{%endhighlight%}

{%highlight ruby%}
UPDATE salary set sex =CHAR((ASCII('f')^ASCII('m')^ASCII(sex)));
{%endhighlight%}