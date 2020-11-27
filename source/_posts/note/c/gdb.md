---
title: GDB 使用
layout: post
comments: true
tags:
    - C
    - gdb
categories:
    - - 笔记
      - C
hidden: true
date: 2020-11-27 10:50:00
updated:
permalink: note/c/gdb
---

# gdb 调试

[笔记索引](note/c/index)

> 部分摘自 [Linux Tools Quick Tutorial - gdb 调试利器](https://linuxtools-rst.readthedocs.io/zh_CN/latest/tool/gdb.html)

善用 gdb 的 `help` 文档

<!--more-->

## 启动 gdb

1. 对 C/C++程序的调试，需要在编译前就加上-g 选项:

```shell
$g++ -g hello.cpp -o hello
```

2. 调试可执行文件:

```shell
$gdb <program>
```

或

```shell
$gdb
(gdb) file program
```

program 为可执行文件名

## gdb 交互命令

启动 gdb 后，进入到交互模式，通过以下命令完成对程序的调试；注意高频使用的命令一般都会有缩写

交互模式下直接回车的作用是重复上一指令

-   运行

    -   `run`（简写 `r`）：运行程序，遇到断点后，程序会在断点处停止运行，等待用户输入下一步的命令
    -   `continue`（简写 `c`）：继续执行，直到下一个断点处
    -   `next`（简写 `n`）：单步调试，当遇到函数调用时，不进入此函数体直接返回
    -   `step` （简写`s`）：单步调试，如果有函数调用，则进入函数
    -   `until`：继续运行程序直到退出循环体
    -   `until 行号`： 运行至某行
    -   `finish`： 运行程序，直到当前函数完成返回，并打印函数返回时的堆栈地址和返回值及参数值等信息
    -   `return 返回值` 立即结束函数并手动设置返回值
    -   `call 函数(参数)`：调用程序中可见的函数，并传递参数，例：`call gdb_test(55)`
    -   `quit`（简写 `q`）：退出 gdb

-   设置断点

    -   `break n`（`break` 简写`b`）：在第`n`行处设置断点，或在指定文件对应行设置断点 `b main.c:578`
    -   `break 函数名`：在函数的入口处设置断点，例：`break main`
    -   `break *内存号`：在内存号处设置断点，例：`break *0x3400a`
    -   `break 行号或者函数名 if a＞b`：条件断点设置
    -   `watch 表达式`：设置一个监视断点，一旦被监视的表达式的值改变，将暂停运行
    -   `delete 断点号n`：删除第 n 个断点
    -   `clear 行号n`：清除第 n 行的断点
    -   `disable 断点号n`：停用第 n 个断点
    -   `enable 断点号n`：启用第 n 个断点
    -   `info breakpoints` （简写 `info b`）：显示当前程序的断点设置情况
    -   `delete breakpoints`：清除所有断点

-   查看源代码

    -   `list`（简写 `l`）：从上一次`list`命令之后，列出程序的源代码，默认每次显示 10 行
    -   `list 行号`：将显示当前文件以此行为中心的前后 10 行代码
    -   `list 函数名`：将显示函数的源代码

-   打印表达式

    -   `print 表达式`（简写 `p`），打印*任何*当前正在被测试程序的有效表达式
    -   `whatis`：查询表达式类型
    -   `display 表达式`：将在每次暂停运行后，自动输出被设置的表达式及值
    -   `undisplay 表达式`：取消 display
    -   `info display` 显示当前所有要显示值的表达式的情况

-   shell

    -   `shell 命令` 来运行 shell 命令
