---
layout: post
title: "PHP数组中的对偶函数"
date: 2017-06-18 10:11:06 +0800
description: PHP的数组中的那些对偶(互反)函数，不断更新
tags: 
 - PHP

---
PHP针对数组，内置了许多可用的函数，其中有一类函数，可以互相作为反操作，例如前文中的排序函数的升降序，这里单独整理出来以备取用。

***
### 数组中的对偶函数表

 | 函数名称       | 函数作用      |  反函数 |
 |:-----------------:|:--------------:|:---------------:|
 | [array_push()](http://php.net/manual/zh/function.array-push.php)       | 入栈      | array_pop() |
 | [array_pop()](http://php.net/manual/zh/function.array-pop.php)     | 出栈      | array_push() |
 | [array_unshift()](http://php.net/manual/zh/function.array-unshift.php)| 入队(数组开头)     | array_shift() |
 | [array_shift()](http://php.net/manual/zh/function.array-shift.php)       | 出队(数组开头)      | array_unshift() |
 | [extract()](http://php.net/manual/zh/function.extract.php)       | 数组拆分变量符号表      |compact() |
 | [compact()](http://php.net/manual/zh/function.compact.php)     | 变量压缩成数组      | extract() |
 | [list()](http://php.net/manual/zh/function.list.php)       | 数组给一组变量赋值     | array() |
 | [array()](http://php.net/manual/zh/function.array.php)  | 新建数组      | list() |

***
