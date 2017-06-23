---
layout: post
title: "LeetCode_181. Employees Earning More Than Their Managers"
date: 2017-06-20 12:21:06 +0800
description: LeetCode 数据库系列，输出高收入员工
tags: 
 - LeetCode_DataBase

---
### 181. Employees Earning More Than Their Managers
The Employee table holds all employees including their managers. Every employee has an Id, and there is also a column for the manager Id.
>+----+-------+--------+-----------+
| Id | Name  | Salary | ManagerId |
+----+-------+--------+-----------+
| 1  | Joe   | 70000  | 3         |
| 2  | Henry | 80000  | 4         |
| 3  | Sam   | 60000  | NULL      |
| 4  | Max   | 90000  | NULL      |
+----+-------+--------+-----------+

Given the Employee table, write a SQL query that finds out employees who earn more than their managers. For the above table, Joe is the only employee who earns more than his manager.
>+----------+
| Employee |
+----------+
| Joe      |
+----------+

---
---
解答：这个比较简单，没啥说的，给出两种方式：
- 子查询：
{%highlight ruby%}
SELECT Name AS Employee FROM Employee as e1 WHERE ManagerId IS NOT NULL 
AND salary >(SELECT salary FROM Employee WHERE Id = e1.ManagerId)
{%endhighlight%}

- 联表查询：
{%highlight ruby%}
select e1.Name as Employee from Employee e1 join Employee e2 
on e1.ManagerId = e2.Id where e1.Salary > e2.Salary
{%endhighlight%}