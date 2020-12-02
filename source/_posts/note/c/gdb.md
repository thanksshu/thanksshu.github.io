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
permalink: /note/c/gdb
---

# gdb 调试

[笔记索引](/note/c/index)

> 部分摘自 [Linux Tools Quick Tutorial - gdb 调试利器](https://linuxtools-rst.readthedocs.io/zh_CN/latest/tool/gdb.html)

**善用 gdb 的 `help` 文档**

<!--more-->

## 启动 gdb

1. 对 C/C++程序的调试，需要在编译前就加上-g 选项:

```shell
$g++ -g hello.cpp -o hello
```

2. 调试可执行文件:

```shell
$gdb <program> [corefile]
```

或

```shell
$gdb
...
(gdb) file <program>
(gdb) core <core-file>
```

program 为可执行文件名
core-file 为 core dump 结果，

## 关于 core

    core dump 意为“磁芯倾印”，是操作系统在进程收到某些信号而终止运行时，将此时进程地址空间的内容以及有关进程状态的其他信息写出的一个磁盘文件
    应使用`ulimit -c unlimited`开启 core dump ，然后执行代码以生成 core 文件

## gdb 交互命令

启动 gdb 后，进入到交互模式，通过以下命令完成对程序的调试；注意高频使用的命令一般都会有缩写

_交互模式下直接回车则重复上一指令_

-   运行

    -   `cd <directory>` 指定工作目录
    -   `pwd` 查看工作目录
    -   `run [参数1 [参数2]...] [流重定向]` (`r`) 给定参数运行程序，默认使用上次的参数
    -   `set args` 设定参数
    -   `show args` 显示参数
    -   `tty <流>` 设定流
    -   `kill` (`k`) 终止被调试进程
    -   `quit` (`q`) 退出 gdb

    ***

    -   `continue` (`c`) 继续执行，直到下一个断点处
    -   `next [行数]`(`n`) 单行调试，当遇到函数调用时，不进入此函数（step-over）
    -   `nexti [指令数]`(`ni`) 单步机器指令调试，step-over
    -   `step [行数]` (`s`) 单行调试，如果有函数调用，进入函数 (step-into)
    -   `stepi [指令数]` (`si`) 单步机器指令调试，step-into
    -   `until` (`u`) 继续运行程序直到退出循环体
    -   `until <行号>` 运行至某行
    -   `finish` (`f`) 运行程序，直到当前函数完成返回，并打印函数返回时的堆栈地址和返回值及参数值等信息
    -   `return <返回值>` 立即结束函数并手动设置返回值
    -   `call <函数(参数)>` 调用程序中可见的函数，并传递参数，例 `call gdb_test(55)`

-   回退调试

    回退调试用于撤销，仅支持少数平台（比如 amd64-linux）

    -   `record` 开启记录以反向调试
    -   `record stop` 停止记录

    -   `set exec-direction (forward/reverse)` 设置运行方向

    与一般调试相同但是方向相反的：

    -   `reverse-continue` (`rc`)
    -   `reverse-finish`
    -   `reverse-next` (`rn`)
    -   `reverse-nexti` (`rni`)
    -   `reverse-step` (`rs`)
    -   `reverse-stepi`

-   设置断点

    遇到断点后，程序会在断点处停止运行，等待用户输入下一步的命令

    -   `break n` (`b`) 在第`n`行处设置断点，或在指定文件对应行设置断点 `b main.c:578`
    -   `break 函数名` 在函数的入口处设置断点，例 `break main`
    -   `break *内存号` 在内存号处设置断点，例 `break *0x3400a`
    -   `break 行号或者函数名 if a＞b` 条件断点设置
    -   `watch 表达式` 设置一个监视断点，一旦被监视的表达式的值改变，将暂停运行
    -   `delete [n]` 删除第 n 个断点
    -   `clear [n]` 清除第 n 行的断点
    -   `disable [n]` 停用第 n 个断点
    -   `enable [n]` 启用第 n 个断点
    -   `info breakpoints` (`info b`) 显示当前程序的断点设置情况

-   堆栈

    -   `backtrace [n]` (`bt`) 打印堆栈帧号及相关信息，`n`有符号，指定打印数
    -   `frame <帧号|地址>` (`f`) 查看堆栈帧详情
    -   `up [n]` (`u`) 向上（帧号更大）
    -   `down [n]` (`d`) 向下（帧号更小）

-   查看源代码

    -   `list` (`l`) 从上一次`list`命令之后，列出程序的源代码，默认每次显示 10 行
    -   `list 行号` 将显示当前文件以此行为中心的前后 10 行代码
    -   `list 函数名` 将显示函数的源代码

-   打印表达式

    -   `print 表达式` (`p`) 打印*任何*当前正在被测试程序的有效表达式
    -   `whatis` 查询表达式类型
    -   `display 表达式` 将在每次暂停运行后，自动输出被设置的表达式及值
    -   `undisplay 表达式` 取消 display
    -   `info display` 显示当前所有要显示值的表达式的情况

-   shell

    -   `shell 命令` 来运行 shell 命令
