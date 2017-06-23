---
layout: post
title: "LeetCode_177 Nth Highest Salary"
date: 2017-06-20 12:11:06 +0800
description: LeetCode 数据库系列，查询第N高的薪水
tags: 
 - LeetCode_DataBase

---
###   177. Nth Highest Salary
Write a SQL query to get the **n<sup>th</sup>** highest salary from the `Employee` table.
>+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+

For example, given the above Employee table, the **n<sup>th</sup>** highest salary where n = 2 is 200. If there is no **n<sup>th</sup>** highest salary, then the query should return null.

>+------------------------+
| getNthHighestSalary(2) |
+------------------------+
| 200                    |
+------------------------+

---
---
解答：和上一题查询第二高薪是一个套路，取第N个数就可以了，需要注意的是`OFFSET`是传入的参数，需要减去1，SQL语句中不能直接运算，要先定义一个局部变量，将偏移先减去1:
{% highlight ruby %}
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
SET N=N-1;
  RETURN (
      # Write your MySQL query statement below.
      SELECT (SELECT DISTINCT salary FROM Employee ORDER BY salary DESC LIMIT N,1) AS result
  );
END
{% endhighlight%}

总结，对空集合继续进行查询，或者函数运算操作，返回`NULL`。