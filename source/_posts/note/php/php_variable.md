---
title: PHP 变量相关
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
permalink: /note/php/variable
---

# PHP 变量

[回到笔记索引](/note/php/index)

-   传值赋值：`$a = 1;`

-   引用赋值：`$b = &$a;` 指向同一内存；只有*有名字*的*变量*才可以

另：PHP 有大量预定义变量，见文档

## 引用

`$a =& $b`

引用使得两个变量名指向同一个内存地址

-   引用传递：可以将一个变量通过引用传递给函数，这样该函数就可以修改其参数的值：

```PHP
function foo(&$var)
{
    $var++;
}

foo($a); // 调用无需引用符号
```

-   引用返回，见函数，不必要则无需使用

-   销毁引用：与销毁变量类似

```PHP
<?php
$a = 1;
$b =& $a;
unset($a);
?>
```

-   `global` 相当于引用全局变量

-   `$this` 永远是调用它的对象的引用

## 作用域

PHP 使用函数作用域

`include` 不会产生新作用域

`global` 关键字可以访问全局作用域

`$GLOBALS['a']` 超全局变量亦可，其在全部作用域中可用

`static` 定义静态，只会进行一次初始化，声明不可以传值表达式

## 可变变量

对形如 `$$a` `${$a}` 赋值可以改变 `a` 的变量名

超全局变量 不能用作可变变量；$this 也不能被动态引用。
