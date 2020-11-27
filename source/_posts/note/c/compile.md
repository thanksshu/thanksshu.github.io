---
title: C 编译流程
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
permalink: note/c/compile
---

# 编译流程

[笔记索引](note/c/index)

编译一般可以分为三个阶段：

## 预处理 Preprocessing

执行预处理语句（#define 等）

## 编译和汇编 Compilation & assembly

经过两步将预处理器产生的代码编译成目标文件（object file）：

1. 代码编译成底层汇编代码。在这一步中，编译器会对代码进行检查优化，指出各种错误

2. 汇编器将上一步生成的汇编代码逐行转换成字节码（也就是机器码）

## 链接 Linking

链接器利用编译器产生的目标文件，生成最终结果

在这一阶段，编译器将把上一阶段中编译器产生的各种目标文件链接起来形成一整个链接库或者可执行文件
