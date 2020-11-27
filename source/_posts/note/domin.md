---
title: 定义域
layout: post
comments: true
tags:
    - 静动态定义域
    - 作用域
categories:
    - 笔记
hidden: false
date: 2020-11-25 22:30:13
updated:
permalink:
---

# 定义域

## 静态定义域

在编译时决定定义域:

<!-- more -->

```
var value = 1;

function foo() {
    console.log(value);
}

function bar() {
    var value = 2;
    foo();
}

bar();

// 结果是 1
```

`foo()` 寻找的是定义 function 时的作用域

## 动态定义域

在运行时决定定义域，上述代码返回 2

`foo()` 寻找的是执行 foo()时位于 bar()内的作用域
