---
title: PHP 类型
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
permalink: note/php/type
---

# PHP 类型

[回到笔记索引](note/php/index)

## 标量类型：

### boolean（布尔型）

FALSE:

-   布尔值 `FALSE` 本身 -整型值 `0`（零）
-   浮点型值 `0.0`（零）
-   空字符串，以及字符串 `"0"`
-   不包括任何元素的数组 - 特殊类型 `NULL`（包括尚未赋值的变量）
-   从空标记生成的 `SimpleXML` 对象

TRUE:

-   其余是 `TRUE`（包括任何资源 和 `NAN`）

### integer（整型）

范围：32 位有符号

表示：

-   小数 decimal : `[1-9][0-9]\* | 0`

-   十六进制 hexadecimal : `0[xX][0-9a-fa-f]+`

-   八进制 octal : `0[0-7]+`

-   二进制 binary : `0b[01]+`

-   整型 integer : `[+-]?decimal | [+-]?hexadecimal | [+-]?octal | [+-]?binary`

转换：

-   用 (int) 或 (integer) 强制转换

-   当从浮点数转换成整数时，将向下取整

-   如果给定的一个数超出了 integer 的范围，将会被解释为 float

-   resource 转为整型时为 分配的唯一资源号

-   布尔 FALSE 将产生出 0 ，TRUE 将产生出 1

-   float（浮点型，也称作 double)

    表示：

    -   `LNUM [0-9]+`

    -   `DNUM ([0-9]_[\.]{LNUM}) | ({LNUM}[\.][0-9]_)`

    -   `EXPONENT_DNUM [+-]?(({LNUM} | {DNUM}) [eE][+-]? {LNUM})`

    `NaN`:

    -   `NAN` 代表着任何不同值，为不可描述，需要 `is_NaN()` 方法

### string（字符串）

PHP 只能支持 256 的字符集，因此不支持 Unicode

表示：

-   单引号 `'`

    只有 `\\` 和 `\'` 会被转义

    在单引号字符串中的变量和特殊字符的转义序列将*不会*被替换

-   双引号 `"`

    可以使用转义

    变量会被解析

-   Heredoc 结构

    Heredoc 可以进行解析操作，使用双引号标记（5.3.0 前不需要）

    Heredocs 结构不能用来初始化类的属性
    PHP 5.3.0 ，此限制仅对 heredoc 包含变量时有效，同时 Heredoc 结构可以初始化静态变量和类的属性和常量，
    示例：

    ```PHP
    <<<"标记"
    My name is "$name". I am printing some $foo->foo.
    Now, I am printing some {$foo->bar[1]}.
    This should print a capital 'A': \x41
    标记;
    ```

    输出：

    My name is "MyName". I am printing some Foo.
    Now, I am printing some Bar2.
    This should print a capital 'A': A

-   Nowdoc 结构

    nowdoc 中不进行解析操作，使用单引号标记

    nowdoc 结构可以用在任意的静态数据环境中

    ```PHP
    <<<'EOT'
    My name is "$name". I am printing some $foo->foo.
    Now, I am printing some {$foo->bar[1]}.
    This should not print a capital 'A': \x41
    EOT;
    ```

    变量解析：

    -   简单规则： `$` 会尽量匹配变量

    -   复杂规则： 使用形如 `{$great}`

其他：

    - 可以像数组一样读取写入

    - 字符串可以用 '.'（点）运算符连接起来

    - 一个值可以通过在其前面加上 (string) 或用 strval() 函数来转变成字符串

      - boolean 的 TRUE 被转换成 string 的 "1"，FALSE 被转换成 "" （空字符串）

      - 一个整数 integer 或浮点数 float 被转换为数字的字面样式的 string

      - 数组 array 总是转换成字符串 "Array"

      - 资源 resource 总会被转变成 "Resource id #1" 这种结构的字符串

      - NULL 总是被转变成空字符串

    - 转为数值时，如果该字符串没有包含 '.'，'e' 或 'E' 并且其数字值在整型的范围之内，该字符串将被当成 integer 来取值。其它所有情况下都被作为 float 来取值

## 复合类型：

### array（数组）

-   定义：

    ```PHP
    <?php
    $array = array(
    "key" => "value",
    "key" => "value",
    );

    // 自 PHP 5.4 起
    $array = [
    "key" => "value",
    "key" => "value",
    ];
    ?>
    ```

    key 可以是 integer 或者 string。value 可以是任意类型

    对于 key：

    -   字符串（整型形式）、布尔、浮点（忽略小数部分）会被尽量转换为整型

    -   Null 会被转换为空字符串

    -   数组和对象不可作为 key

    -   为可选项，当未指定时，会自动命名

    -   访问与赋值

        -   访问可以使用 `['$i']` 或 `{'$1'}`，注意引号

        -   赋值就那个样子，删除使用 `unset()` 方法

            _赋值时，注意自动命名_

    -   转换

        -   如果将一个值转换为数组，将得到一个仅有一个元素的数组，其下标为 0

        -   如果一个 object 类型转换为 array，则结果为一个数组，_会导致一些不可预知的行为_

        -   将 NULL 转换为 array 会得到一个空的数组

### object（对象）

-   声明

    ```PHP
    <?php
    class foo {
        function do_foo() {
           echo "Doing foo.";
        }
    }

    $bar = new foo;
    $bar->do_foo();
    ?>
    ```

    详见面向对象

-   转换

-   如果其它任何类型的值被转换成对象，将会创建一个内置类 stdClass 的实例

-   如果该值为 NULL，则新的实例为空

-   array 转换成 object 将使键名成为属性名并具有相对应的值

-   对于其他值，会包含进成员变量名 scalar

### callable（可调用）

-   自 PHP 5.4 起可用 callable 类型指定回调类型 callback

-   PHP 是将函数以 string 形式传递的，一个已实例化的 object 的方法被作为 array 传递，下标 0 包含该 object，下标 1 包含方法名。 在同一个类里可以访问 protected 和 private 方法

```PHP
// Type 1: Simple callback
call_user_func('my_callback_function');

// Type 2: Static class method call
call_user_func(array('MyClass', 'myCallbackMethod'));

// Type 3: Object method call
$obj = new MyClass();
call_user_func(array($obj, 'myCallbackMethod'));
```

## 伪类型：

并不是实际存在的类型，而是类型的集合

### mixed（混合类型）

一个参数可以接受多种不同的（但不一定是所有的）类型

### number（数字类型）

一个参数可以是 integer 或者 float

### callback（回调类型，又称为 callable）

PHP 5.4 引入 callable 类型之前使用 了 callback 伪类型

### array|object（数组 | 对象类型）

字面意思

### void （无类型）

无返回值或不接受参数

### 伪变量

`$...`当一个函数可以接受任意个参数时使用此变量名
`

## 特殊类型：

### resource（资源）

资源 resource 是一种特殊变量，保存了到外部资源的一个引用。

### NULL（无类型）

特殊的 NULL 值表示一个变量没有值。NULL 类型唯一可能的值就是 NULL：

-   被赋值为 NULL。

-   尚未被赋值。

-   被 unset()。

## 数据类型

-   double 和 float 是相同的

-   PHP 使用鸭子类型

-   如果想查看某个表达式的值和类型，用 var_dump() 函数

-   如果只是想得到一个易读懂的类型的表达方式用于调试，用 gettype() 函数。要检验某个类型，不要用 gettype()，而用 is_type 函数

-   对其使用 强制转换 或者 settype() 函数，可以转换类型：

    -   强制转换有：

        -   (int), (integer) - 转换为整形 integer

        -   (bool), (boolean) - 转换为布尔类型 boolean

        -   (float), (double), (real) - 转换为浮点型 float

        *   (string) - 转换为字符串 string

        *   (array) - 转换为数组 array

        *   (object) - 转换为对象 object

        *   (unset) - 转换为 NULL (PHP 5)

        -   (binary) - 转换为 二进制 (PHP 5.2.1)

-   变量根据其当时的类型在特定场合下会表现出不同的值。
