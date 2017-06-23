---
layout: post
title: "LeetCode_596. Classes More Than 5 Students"
date: 2017-06-23 10:21:06 +0800
description: LeetCode 数据库系列，那些超过5个学生的班级
tags: 
 - LeetCode_DataBase

---
###  596. Classes More Than 5 Students
There is a table courses with columns: student and class

Please list out all classes which have more than or equal to 5 students.

For example, the table:

For example:

>+---------+------------+
| student | class      |
+---------+------------+
| A       | Math       |
| B       | English    |
| C       | Math       |
| D       | Biology    |
| E       | Math       |
| F       | Computer   |
| G       | Math       |
| H       | Math       |
| I       | Math       |
+---------+------------+

Should output:

>+---------+
| class   |
+---------+
| Math    |
+---------+
Note:
The students should not be counted duplicate in each course.

---
---

解答：输出超过5个学生班级即可，没注意Note里说不可重复计算学生数量，用例里面也确实出现了重复项，加上`DISTINCT`就可以了：
- 一般方法：

{% highlight ruby%}
SELECT class FROM courses GROUP BY class HAVING COUNT(DISTINCT student) >= 5;
{% endhighlight %}


- 子查询

{% highlight ruby%}
SELECT class FROM (SELECT COUNT(DISTINCT student) AS num,class FROM courses GROUP BY class) AS T WHERE T.num>=5;
{% endhighlight %}