---
title: PHP 常量
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
permalink: /note/php/constant
---

# 常量

[回到笔记索引](/note/php/index)

-   常量前面没有美元符号 `echo CONSTANT;`

-   只能包含标量数据

-   使用形如 `define("FOO","something");` 定义常量，PHP 5.3.0 以后，可以使用 `const` 关键字

-   全部作用域可用

## 魔术常量

有值随着它们在代码中的位置改变而改变：

-   `__LINE__` 文件中的当前行号。
-   `__FILE__` 文件的完整路径和文件名；自 PHP 4.0.2 总是包含一个绝对路径
-   `__DIR__` 文件所在的目录（PHP 5.3.0 中新增）
-   `__FUNCTION__` 函数名称，返回该函数被定义时的名字（区分大小写）
-   `__CLASS__` 类的名称，返回该类被定义时的名字（区分大小写）；类名包括其被声明的作用区域（例如 Foo\Bar）；自 PHP 5.4 起对 Trait 也起作用，调用 trait 方法的类的名字。
-   `__TRAIT__` Trait 的名字（PHP 5.4.0 新加）；返回 trait 被定义时的名字（区分大小写）。Trait 名包括其被声明的作用区域（例如 Foo\Bar）
-   `__METHOD__` 类的方法名（PHP 5.0.0 新加）；返回该方法被定义时的名字（区分大小写）
-   `__NAMESPACE__` 当前命名空间的名称（区分大小写）；此常量是在编译时定义的（PHP 5.3.0）
