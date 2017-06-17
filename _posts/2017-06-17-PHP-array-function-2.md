---
layout: post
title: "PHP数组中的高阶函数"
date: 2017-06-16 14:11:06 +0800
description: PHP的数组相关的排序算法
tags: 
 - PHP

---
PHP针对数组，内置了许多可用的函数，其中有一类函数，可以针对每个数组中的元素进行操作，属于函数式编程中的高阶函数。

***
### 数组中的高阶函数表

 | 函数名称       | 函数作用      |
 |:-----------------:|:--------------:|
 | array_filter()       | 过滤数组中的单元      |
 | array_map()       | 为每个元素应用回调函数      |
 | array_reduce()       | 过滤数组中的单元      |
 | array_walk()       | 过滤数组中的单元      |

***

(1)[array_filter](http://us1.php.net/manual/zh/function.array-filter.php)
  用回调函数过滤数组张的单元。
  
{% highlight php %}
<?php
array array_filter ( array $array [, callable $callback [, int $flag = 0 ]] )
?>
{% endhighlight %}

   依次将`array`数组中的每个值传递到`callback`函数，如果`callback`函数返回`true`，则`array`数组中的当前值会被包含再返回的结果数组中，。数组的键名保持不变。
   - array 要循环的数组
   - callback 使用的回掉函数，默认删除`array`中的所有等值为`false`的条目。
   - flag 决定`callback`的过滤方式，
     - `ARRAY_FILTER_USR_KEY` 仅过滤键名
     - `ARRAY_FILTER_USR_BOTH` 同时过滤键名和键值
 
 例：数组按奇数偶数分组：
  {% highlight php linenos %}
<?php
function odd($var)
{
    // returns whether the input integer is odd
    return($var & 1);
}

function even($var)
{
    // returns whether the input integer is even
    return(!($var & 1));
}

$array1 = array("a"=>1, "b"=>2, "c"=>3, "d"=>4, "e"=>5);
$array2 = array(6, 7, 8, 9, 10, 11, 12);

echo "Odd :\n";
print_r(array_filter($array1, "odd"));
echo "Even:\n";
print_r(array_filter($array2, "even"));
?>
{% endhighlight %}
注意：不可以再回调函数中修改数组本身。如果，数组变化了，函数行为不可预测。
(2)[array_map()](http://us1.php.net/manual/zh/function.array-map.php)

{% highlight php %}
<?php
array array_map ( callable $callback , array $array1 [, array $... ] )
?>
{% endhighlight %}
`array_map():`返回数组，是为 `array1` 每个元素应用 `callback`函数之后的数组。 `callback` 函数形参的数量和传给 `array_map()` 数组数量，两者必须一样。