---
layout: post
title: "LeetCode_178. Rank Scores"
date: 2017-06-20 12:21:06 +0800
description: LeetCode 数据库系列，分数排序
tags: 
 - LeetCode_DataBase

---
###  178. Rank Scores
Write a SQL query to rank scores. If there is a tie between two scores, both should have the same ranking. Note that after a tie, the next ranking number should be the next consecutive integer value. In other words, there should be no "holes" between ranks.
>+----+-------+
| Id | Score |
+----+-------+
| 1  | 3.50  |
| 2  | 3.65  |
| 3  | 4.00  |
| 4  | 3.85  |
| 5  | 4.00  |
| 6  | 3.65  |
+----+-------+

For example, given the above Scores table, your query should generate the following report (order by highest score):

>+-------+------+
| Score | Rank |
+-------+------+
| 4.00  | 1    |
| 4.00  | 1    |
| 3.85  | 2    |
| 3.65  | 3    |
| 3.65  | 3    |
| 3.50  | 4    |
+-------+------+

---
---
解答：本题查出`Score`没有难度，难在如何增加Rank列：
{% highlight ruby %}
SELECT Score,(SELECT COUNT(DISTINCT score) FROM Scores WHERE score >= tb_org.score) AS Rank FROM Scores AS tb_org ORDER BY Score DESC;
END
{% endhighlight%}
