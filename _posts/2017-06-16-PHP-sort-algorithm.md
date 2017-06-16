---
layout: post
title: "PHP数组排序算法汇总"
date: 2017-06-16 14:11:06 +0800
description: PHP的数组相关的排序算法
tags: 
 - PHP

---
PHP针对数组，内置了许多可用的函数，而排序函数更是重中之重。以下内容摘自官方文档，部分添加了个人理解。
两点需要注意的地方：
1. 数组的所有排序函数都是直接作用于数组本身的，并不是返回新的有序数组。
2. 排序后的数组顺序是不稳定的，也就是说相等元素的位置不稳定(底层是用快排实现的)。
#### [排序函数比较表](http://us1.php.net/manual/zh/array.sorting.php)
| 函数名称       | 排序依据      |数组索引键保持   |排序的顺序   |相关的函数   |
|:------------------:|:---------:|:-------------:|:---------:|:--------:|
|`array_multisort`   |   值    |键值关联的保持，数字不保持|第一个数组或者指定选项|`array_walk()`         |
|`asort`|   值   |   是   |  ASC   |  `arsort()`  |
|`arsort`|   值   |   是   |  DESC   |  `asort()`  |
|`natcasesort()`|   值   |   是   |  自然排序，大小写不敏感   |  `natsort()`  |
|`natsort`|   值   |   是   |  自然排序   |  `natcasesort()`  |
|`sort`|   值   |   `否`   |  ASC   |  `rsort()`  |
|`rsort`|   值   |   `否`   |  DESC   |  `sort()`  |
|`usort`|   值   |   `否`   |  用户定义   |  `uasort()`  |
|`uasort`|   值   |   是   |  用户定义   |  `uksort()`  |
|`shuffle()`|   值   |   `否`   |  随机   |  `array_rand()`  |
|`ksort()`|   键   |   是   |  ASC   |  `krsort()`  |
|`krsort()`|   键   |   是   |  DESC   |  `krort()`  |
|`uksort()`|   键   |   是   |  用户定义   |  `uasort()`  |
