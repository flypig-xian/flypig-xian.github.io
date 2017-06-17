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
1. 数组的所有排序函数都是`直接作用于数组本身`的，并不是返回新的有序数组。
2. 排序后的数组顺序是`不稳定`的，也就是说相等元素的位置不稳定(底层是用快排实现的)。

***
### > [排序函数比较表](http://us1.php.net/manual/zh/array.sorting.php)

| 函数名称       | 排序依据      |数组索引键保持   |排序的顺序   |相关的函数   |
|:------------------:|:---------:|:-------------:|:---------:|:--------:|
|**array_multisort()**|   值    |键值关联的保持，数字不保持|第一个数组或指定选项|**array_walk()**         |
|**asort()**|   值   |   是   |  ASC   |  **arsort()**  |
|**arsort()**|   值   |   是   |  DESC   |  **asort()**  |
|**natcasesort()**|   值   |   是   |  自然排序，大小写不敏感   |  **natsort()**  |
|**natsort()**|   值   |   是   |  自然排序   |  **natcasesort()**  |
|**sort()**|   值   |   `否`  |  ASC   |  **rsort()**  |
|**rsort()**|   值   |   `否`  |  DESC   |  **sort()**  |
|**usort()**|   值   |   `否`  |  用户定义   |  **uasort()**  |
|**uasort()**|   值   |   是   |  用户定义   |  **uksort()**  |
|**shuffle()**|   值   |   `否`   |  随机   |  **array_rand()**  |
|**ksort()**|   键   |   是   |  ASC   |  **krsort()**  |
|**krsort()**|   键   |   是   |  DESC   |  **krort()**  |
|**uksort()**|   键   |   是   |  用户定义   |  **uasort()**  |

---
- `array_multisort()`:多个数组依次排序或者多维数组排序，默认升序，第一个数组是排序的主要数组，类似于mysql中的主键，而这个函数的功能和`order by`非常相似。
官方文档有两个非常典型的例子，这里做个标记：
- 不区分大小写字母排序：
   将原数组转化为小写后，再以此作为排序标志对原数组排序。
    {% highlight php linenos %}
    <?php
    $array = array('Alpha', 'atomic', 'Beta', 'bank');
    $array_lowercase = array_map('strtolower', $array);

    array_multisort($array_lowercase, SORT_ASC, SORT_STRING, $array);

    print_r($array);
    ?>
    {% endhighlight %}
   - 对数据库结果(多维)进行排序
   本例中的data数组的每一个单元表示一个表中的一行，是典型的数据库的数据集合(通常是通过`mysql_fetch_assoc`循环获得)。
    {% highlight php linenos %}
     <?php
    $data[] = array('volume' => 67, 'edition' => 2);
    $data[] = array('volume' => 86, 'edition' => 1);
    $data[] = array('volume' => 85, 'edition' => 6);
    $data[] = array('volume' => 98, 'edition' => 2);
    $data[] = array('volume' => 86, 'edition' => 6);
    $data[] = array('volume' => 67, 'edition' => 7);
        // 取得列的列表
    foreach ($data as $key => $row) {
        $volume[$key]  = $row['volume'];
        $edition[$key] = $row['edition'];
    }

    // 将数据根据 volume 降序排列，根据 edition 升序排列
    // 把 $data 作为最后一个参数，以通用键排序
    array_multisort($volume, SORT_DESC, $edition, SORT_ASC, $data);

    ?>
    {% endhighlight %}

   首先取出多维数组的两列，然后函数会将第一列按照降序排列，再将第二列中对应第一列相同的部分按照升序排序，则这个二维数组就有序了。
   
   例2中的取多维数组的列操作也可以直接采用PHP中的内置函数`array_column`函数来实现。
   
    {% highlight php %}
    <?php
   array array_column ( array $input , mixed $column_key [, mixed $index_key = null ] )
    {% endhighlight %}
   `array_column()` 返回input数组中键值为`column_key`的列， 如果指定了可选参数`index_key`，那么`input`数组中的这一列的值将作为返回数组中对应值的键。