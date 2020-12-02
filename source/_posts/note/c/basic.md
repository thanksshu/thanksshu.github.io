---
title: C 代码结构
layout: post
comments: true
tags:
    - C
categories:
    - - 笔记
      - C
hidden: true
date: 2020-11-27 10:50:00
updated:
permalink: /note/c/basic
---

# C 代码结构

[笔记索引](/note/c/index)

```c
#include <stdio.h> // 加载头文件

/* 多行注释 */
// 单行注释

int main(int argc, char *argv[]) // 返回值为 int，接受两个命令行参数
{
    int age = 10; // 变量声明
    int height = 72;

    printf("I am %d years old.\n", age); // C 风格输出格式化
    printf("I am %d inches tall.\n", height);

    return 0; // 返回值
}
```

<!-- more -->

```
    I am 10 years old.
    I am 72 inches tall.
```
