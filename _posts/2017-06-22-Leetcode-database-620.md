---
layout: post
title: "LeetCode_620. Not Boring Movies"
date: 2017-06-22 10:21:06 +0800
description: LeetCode 数据库系列，寻找好电影
tags: 
 - LeetCode_DataBase

---
### 620. Not Boring Movies
X city opened a new cinema, many people would like to go to this cinema. The cinema also gives out a poster indicating the movies’ ratings and descriptions.

Please write a SQL query to output movies with an odd numbered ID and a description that is not 'boring'. Order the result by rating.

For example, table `cinema`:

>+---------+-----------+--------------+-----------+
|   id    | movie     |  description |  rating   |
+---------+-----------+--------------+-----------+
|   1     | War       |   great 3D   |   8.9     |
|   2     | Science   |   fiction    |   8.5     |
|   3     | irish     |   boring     |   6.2     |
|   4     | Ice song  |   Fantacy    |   8.6     |
|   5     | House card|   Interesting|   9.1     |
+---------+-----------+--------------+-----------+

For the example above, the output should be:

>+---------+-----------+--------------+-----------+
|   id    | movie     |  description |  rating   |
+---------+-----------+--------------+-----------+
|   5     | House card|   Interesting|   9.1     |
|   1     | War       |   great 3D   |   8.9     |
+---------+-----------+--------------+-----------+

---
---

解答：非常简单，没啥说的，一次搞定,这里取奇数有多种方式，MARK一下：
>mod(id,2)=1,
>id%2=1
>id&1
{%highlight ruby%}
# Write your MySQL query statement below
SELECT id,movie,description,rating FROM cinema WHERE  (id&1 AND description != 'boring') ORDER BY rating DESC;
{%endhighlight%}