---
layout: post
title: "LeetCode_180. Consecutive Numbers"
date: 2017-06-20 12:21:06 +0800
description: LeetCode 数据库系列，连续数字
tags: 
 - LeetCode_DataBase

---
### 180. Consecutive Numbers
Write a SQL query to find all numbers that appear at least three times consecutively.
>+----+-----+
| Id | Num |
+----+-----+
| 1  |  1  |
| 2  |  1  |
| 3  |  1  |
| 4  |  2  |
| 5  |  1  |
| 6  |  2  |
| 7  |  2  |
+----+-----+
+----+-------+

For example, given the above `Logs` table, `1` is the only number that appears consecutively for at least three times.
>+-----------------+
| ConsecutiveNums |
+-----------------+
| 1               |
+-----------------+

---
---
解答：这道题有点点坑，因为没有说明`Id`是否连续，虽然题目默认是连续的。
一开始没有申请题，认为只是提取数量超过3个的，用了下面这个查询语句：
{% highlight ruby %}
SELECT Num AS ConsecutiveNums from Logs GROUP BY Num HAVING COUNT(Num) >3
{% endhighlight%}

题目的关键在于连续取三行数据，且要保证数目相等，`ID`默认连续，语句如下：
{% highlight ruby %}
SELECT l1.Num AS ConsecutiveNums from Logs l1,Logs l2,Logs l3
WHERE l1.num =l2.num AND l2.num=l3.num AND l1.Id = l2.Id+1 AND l2.Id = l3.Id+1
{% endhighlight%}
等于数据表自身内连接了两次，取数字相同且ID连续3个的记录。