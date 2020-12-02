---
title: PHP 函数
layout: post
comments: true
tags:
    - PHP
categories:
    - - 笔记
      - PHP
hidden: true
date: 2020-11-27 12:00:00
updated:
permalink: /note/php/function
---

# 函数

[回到笔记索引](/note/php/index)

```PHP
<?php
function foo($arg_1, $arg_2, /* ..., */ $arg_n)
{
    echo "Example function.\n";
    return $retval;
}
?>
```

-   PHP 中的所有函数和类都具有全局作用域

-   PHP 不支持函数重载，也不可能取消定义或者重定义已声明的函数

-   传参可以传值 `$value`，也可以引用 `&$value` 后者可以直接访问变量

-   默认传参形式：`$type = XXX`，默认值必须是常量表达式，任何默认参数必须放在任何非默认参数的右侧

## 传参

```PHP
<?php
 function test(boolean $param) {}
 test(true);
 ?>
```

-   上述格式可以限制传参类型

-   通过`declare` 严格类型，不再对函数传参进行自动转换，见[严格类型](https://www.php.net/manual/zh/functions.arguments.php#functions.arguments.type-declaration.strict)

---

```PHP
<?php
function sum(...$numbers) {
    $acc = 0;
    foreach ($numbers as $n) {
        $acc += $n;
    }
    return $acc;
}

echo sum(1, 2, 3, 4);
?>
```

-   （PHP 5.6）通过 `...` 传递可变数量的参数列表

```PHP
<?php
function sum() {
    $acc = 0;
    foreach (func_get_args() as $n) {
        $acc += $n;
    }
    return $acc;
}

echo sum(1, 2, 3, 4);
?>
```

-   （PHP 5.5 -）使用函数 func_num_args()，func_get_arg()，和 func_get_args()

## 返回值

-   函数不能返回多个值，但可以通过返回一个数组来得到类似的效果

-   从函数返回一个引用，必须在函数声明和指派返回值给一个变量时都使用引用运算符 &

```PHP
<?php
function &returns_reference()
{
    return $someref;
}

$newref =& returns_reference();
?>
```

-   （PHP 7）可以指定返回值，受到 严格类型 影响

```PHP
<?php
function sum($a, $b): float {
    return $a + $b;
}
?>
```

可变函数

```PHP
$func = 'foo';
$func(); // 调用 foo()

$func = 'bar';
$func();  // 调用 bar()

$func = array("Foo", "bar");
$func(); // 调用了 Foo 类的 bar() 静态方法
// 或者表示 调用了 Foo 实例的 bar() 成员对象
```

-   也可以用可变函数的语法来调用一个对象的方法

## 匿名（闭包）函数（PHP 5.3）

```PHP
<?php
// 将匿名函数赋值给变量
$greet = function($name)
{
    printf("Hello %s\r\n", $name);
};

$greet('World');
?>
```

```PHP
$example = function () use ($message) {
    var_dump($message); // 闭包继承父定义域
};
echo $example();
```

-   （PHP 5.4）对匿名函数使用 `static` 可以防止类对其绑定（变量 $this）

## 生成器

`yield` 关键字：

-   `yield $id;` `$data = (yield $value);`

-   `yield $id => $fields;` `$data = (yield $key => $value);` 指定键名

-   `yield;` 返回 NULL

-   生成器返回的迭代对象可以迭代引用变量：

    ```PHP
    function &gen_reference() {
        $value = null;
        yield $value;

    }
    ```

-   `yield from` 调用另外的可迭代对象
