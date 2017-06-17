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

 | 函数名称       | 函数作用      |  特点|
 |:-----------------:|:--------------:|:---------------:|
 | array_filter()       | 过滤数组中的单元      |返回数组，作用于第一维|
 | array_map()       | 为每个元素应用回调函数      | 返回数组，可作用于多个数组，生成多维数组|
 | array_reduce()       | 用回调函数迭代地将数组简化为单一的值      |返回混合类型|
 | array_walk()       | 使用自定义的函数处理数组中的每个元素      | 直接作用于自身，可通过&修改数组，有递归形式array_walk_recursice()|

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
`array_map():`返回数组，是为 `array1` 每个元素应用 `callback`函数之后的数组。 `callback` 函数形参的数量和传给 `array_map()` 的数组数量，两者必须一样。
例一：使用多个数组
{% highlight php linenos%}
<?php
function show_Spanish($n, $m)
{
    return("The number $n is called $m in Spanish");
}

function map_Spanish($n, $m)
{
    return(array($n => $m));
}

$a = array(1, 2, 3, 4, 5);
$b = array("uno", "dos", "tres", "cuatro", "cinco");

$c = array_map("show_Spanish", $a, $b);
print_r($c);

$d = array_map("map_Spanish", $a , $b);
print_r($d);
?>
{% endhighlight %}

传入两个及以上的数组时，它们元素数量将会相同。因为回调函数会并行地处理相互对应的元素。 如果几个数组的元素数量不一致：空元素会扩展短那个数组，直到长度和最长的数组一样。

`此函数有个有趣的用法：传入 NULL 作为回调函数的名称，将创建多维数组。`

例2：索引(键名)是string类型：
如果仅传入一个数组，键（key）会保留；传入多个数组，键（key）是整型数字的序列。

{% highlight php linenos%}
<?php
$arr = array("stringkey" => "value");
function cb1($a) {
    return array ($a);
}
function cb2($a, $b) {
    return array ($a, $b);
}
var_dump(array_map("cb1", $arr));//键名仍是stringkey
var_dump(array_map("cb2", $arr, $arr));//键名成为数组0
var_dump(array_map(null,  $arr));//单个数组，保持不变
var_dump(array_map(null, $arr, $arr));//多个数组合并为多维数组，键值为数字
?>
{% endhighlight %}

(3)[array_reduce()](http://php.net/manual/zh/function.array-reduce.php)
将回调函数迭代的作用到每个元素上，最后返回一个最终结果。
{% highlight php %}
<?php
mixed array_reduce ( array $array , callable $callback [, mixed $initial = NULL ] )
?>
{% endhighlight %}
例：
{% highlight php linenos %}
<?php
function sum($carry, $item)
{
    $carry += $item;
    return $carry;
}

function product($carry, $item)
{
    $carry *= $item;
    return $carry;
}

$a = array(1, 2, 3, 4, 5);
$x = array();

var_dump(array_reduce($a, "sum")); // int(15)
var_dump(array_reduce($a, "product", 10)); // int(1200), because: 10*1*2*3*4*5
var_dump(array_reduce($x, "sum", "No data to reduce")); //输出初始值 string(17) "No data to reduce"
?>
{% endhighlight %}

(4)[array_walk()](http://php.net/manual/zh/function.array-walk.php)
{% highlight php %}
<?php
bool array_walk ( array &$array , callable $callback [, mixed $userdata = NULL ] )
?>
{% endhighlight %}
将用户自定义函数 `funcname` 应用到 `array` 数组中的每个单元。
`array_walk()` 不会受到 `array` 内部数组指针的影响。`array_walk()` 会遍历整个数组而不管指针的位置。

- callback
典型情况下 `callback` 接受两个参数。array 参数的值作为第一个，键名作为第二个。
  - 如果 `callback` 需要直接作用于数组中的值，则给 `callback` 的第一个参数指定为引用。这样任何对这些单元的改变也将会改变原始数组本身。
  - 参数数量超过预期，传入内置函数 (例如 `strtolower()`)， 将抛出警告，所以不适合当做 `funcname`。

例：
{% highlight php linenos %}
<?php
$fruits = array("d" => "lemon", "a" => "orange", "b" => "banana", "c" => "apple");

function test_alter(&$item1, $key, $prefix)
{
    $item1 = "$prefix: $item1";
}

function test_print($item2, $key)
{
    echo "$key. $item2<br />\n";
}

echo "Before ...:\n";
array_walk($fruits, 'test_print');//修改前，输出数组原始key=>value值

array_walk($fruits, 'test_alter', 'fruit');//给数组的键名添加fruit前缀
echo "... and after:\n";

array_walk($fruits, 'test_print');//再次打印，输出数组修改后的fruit:key=>value值
?>
{% endhighlight %}