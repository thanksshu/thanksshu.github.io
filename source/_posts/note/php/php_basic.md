---
title: PHP 基本
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
permalink: /note/php/basic
---

# 基础概念

[回到笔记索引](/note/php/index)

-   从 HTML 模式进入 PHP 模式

```PHP
<?php //标记开始
// 注释
/* 多行注释 */
// 下一行为标记结束，如果是纯脚本可以省略
?>
```

-   PHP 使用语法定义域

-   PHP 为函数作用域

## 一些记录

-   `exit()` 将停止整个线程，如果要在 `include` 中返回父级，使用 `return`
-   `isset()` 判断是否定义、`empty()` 判断是否定义或空、`is_null()` 判断是否为 `null`
