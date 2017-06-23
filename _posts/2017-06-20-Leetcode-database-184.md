---
layout: post
title: "LeetCode_184. Department Highest Salary"
date: 2017-06-20 15:21:06 +0800
description: LeetCode 数据库系列，输出各部门的最高薪水
tags: 
 - LeetCode_DataBase

---
### 184. Department Highest Salary
The Employee table holds all employees. Every employee has an Id, a salary, and there is also a column for the department Id.

>+----+-------+--------+--------------+
| Id | Name  | Salary | DepartmentId |
+----+-------+--------+--------------+
| 1  | Joe   | 70000  | 1            |
| 2  | Henry | 80000  | 2            |
| 3  | Sam   | 60000  | 2            |
| 4  | Max   | 90000  | 1            |
+----+-------+--------+--------------+

The Department table holds all departments of the company.

>+----+----------+
| Id | Name     |
+----+----------+
| 1  | IT       |
| 2  | Sales    |
+----+----------+

Write a SQL query to find employees who have the highest salary in each of the departments. For the above tables, Max has the highest salary in the IT department and Henry has the highest salary in the Sales department.
>+------------+----------+--------+
| Department | Employee | Salary |
+------------+----------+--------+
| IT         | Max      | 90000  |
| Sales      | Henry    | 80000  |
+------------+----------+--------+

---
---

解答：输出各部门的最大薪水：
- 子查询+连接查询：
{%highlight ruby%}
# Write your MySQL query statement below
SELECT D.Name AS Department ,E.Name AS Employee ,E.Salary 
FROM Employee E,(SELECT DepartmentId,max(Salary) as max FROM Employee GROUP BY DepartmentId) T, Department D 
WHERE E.DepartmentId = T.DepartmentId AND E.Salary = T.max AND E.DepartmentId = D.id
{%endhighlight%}
其实就是分组查出最大薪水，然后和雇员表、部门表内联后输出。

-还有一个思路，雇员表内联部门表后，从最大薪水表用`IN`过滤：
{% highlight ruby %}
# Write your MySQL query statement below
SELECT D.Name AS Department ,E.Name AS Employee ,E.Salary 
FROM department D,Employee E WHERE D.Id=E.departmentId AND (D.Id,E.Salary) IN( SELECT DepartmentId,MAX(salary) FROM Employee GROUP BY DepartmentId)
{%endhighlight%}