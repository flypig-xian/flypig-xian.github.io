---
layout: post
title: "LeetCode_176 Second Highest Salary"
date: 2017-06-20 11:11:06 +0800
description: LeetCode 数据库系列，查询第二高的薪水
tags: 
 - LeetCode_DataBase

---
###   176. Second Highest Salary
Write a SQL query to get the second highest salary from the `Employee` table.
>+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+

For example, given the above Employee table, the query should return 200 as the second highest salary. If there is no second highest salary, then the query should return `null`.

>+---------------------+
| SecondHighestSalary |
+---------------------+
| 200                 |
+---------------------+

---
---
解答：这道查询的关键在于，如果没有存在第二高的薪水值，需要返回空，看了大家的讨论，有以下两种解决方案:
1. 利用`UNION`操作符，将查表结果与`NULL`进行合并，然后输出：
	{% highlight php %}
# Write your MySQL query statement below
(SELECT DISTINCT salary AS SecondHighestSalary FROM Employee  ORDER BY SecondHighestSalary DESC LIMIT 1,1) UNION SELECT NULL LIMIT 0,1;
{% endhighlight%}

2. 利用`MAX()`函数返回`NULL`

	{% highlight php %}
# Write your MySQL query statement below
SELECT max(salary) AS SecondHighestSalary FROM Employee WHERE salary<(SELECT MAX(salary) FROM Employee);
{% endhighlight%}

3.很巧妙的多用一次`SELECT`:
{% highlight php %}
# Write your MySQL query statement below
SELECT (SELECT DISTINCT salary FROM Employee ORDER BY DESC salary LIMIT 1,1) AS SecondHighestSalary;
{% endhighlight%}

总结，对空集合继续进行查询，或者函数运算操作，返回`NULL`。