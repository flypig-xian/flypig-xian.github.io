---
layout: post
title: "LeetCode_185. Department Top Three Salaries"
date: 2017-06-20 17:21:06 +0800
description: LeetCode 数据库系列，输出各部门的前三高薪
tags: 
 - LeetCode_DataBase

---
### 185. Department Top Three Salaries
The Employee table holds all employees. Every employee has an Id, and there is also a column for the department Id.

>+----+-------+--------+--------------+
| Id | Name  | Salary | DepartmentId |
+----+-------+--------+--------------+
| 1  | Joe   | 70000  | 1            |
| 2  | Henry | 80000  | 2            |
| 3  | Sam   | 60000  | 2            |
| 4  | Max   | 90000  | 1            |
| 5  | Janet | 69000  | 1            |
| 6  | Randy | 85000  | 1            |
+----+-------+--------+--------------+

The Department table holds all departments of the company.

>+----+----------+
| Id | Name     |
+----+----------+
| 1  | IT       |
| 2  | Sales    |
+----+----------+

Write a SQL query to find employees who earn the top three salaries in each of the department. For the above tables, your SQL query should return the following rows.
>+------------+----------+--------+
| Department | Employee | Salary |
+------------+----------+--------+
| IT         | Max      | 90000  |
| IT         | Randy    | 85000  |
| IT         | Joe      | 70000  |
| Sales      | Henry    | 80000  |
| Sales      | Sam      | 60000  |
+------------+----------+--------+

---
---

解答：上一题的增强版，要输出前三高的薪水(薪水不重复)，：
- 子查询+连接查询：
{%highlight ruby%}
# Write your MySQL query statement below
SELECT d.Name AS Department, e.Name AS Employee, e.Salary FROM Employee e
JOIN Department d on e.DepartmentId = d.Id
WHERE (SELECT COUNT(DISTINCT Salary) FROM Employee WHERE Salary > e.Salary
AND DepartmentId = d.Id) < 3 ORDER BY d.Name, e.Salary DESC;
{%endhighlight%}
这个不是很好理解，问题的关键在于子查询这里，取同一部门的所有薪水超过当前比较薪水的个数要小于3，即0,1,2，然后输出`e.salary`,也就是取出部门的最高，次高和第三高的薪水。