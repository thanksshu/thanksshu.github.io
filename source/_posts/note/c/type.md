---
title: C 数据类型
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
permalink: note/c/type
---

# 数据类型

[笔记索引](note/c/index)

## “定义”、“声明”、“赋值”与”初始化“

-   declaration

    声明：说明了变量的名字和类型，但并不分配存储空间

-   definition

    定义：说明了变量的名字和类型，为它分配了存储空间，但并不一定要填充初始值

-   initialization

    初始化：是一种仅对全局变量（全局变量指所有函数外部）、静态变量进行的特殊的定义，若不指定初始值，则自动填充`0`的隐式转换；由于不对局部变量进行，局部变量内定义后，若不赋值，则会留有垃圾值

-   assignment

    赋值：将某一个数值赋给一个变量的过程，赋值只针对于*已定义的*变量，可以多次进行。

<!--more-->

## 基本类型

使用形如 `extern const int name;` 声明

`extern const int name = XXX;` 声明并初始化

`name = XXX` 赋值

-   整型（整数）

    分为`signed`、`unsigned`即有、无符号两种，默认有

    -   长整型

        -   使用`long`声明

        -   长度为 4 或 8 字节

        -   常量

            -   `123l`

            -   `123ul` 无符号

    -   整型

        -   使用`int`声明

        -   长 4 字节

        -   常量

            -   `123u` 无符号

            -   `0xFF` 十六进制

            -   `035` 八进制

            -   `123` 十进制

    -   短整型

        使用`short`声明

        长 2 字节

-   浮点（IEEE 754）

    -   单精度

        -   使用`float`声明

        -   长 4 字节，保证 6 位十进制精度

        -   常量

            -   `2e-3` 科学计数法

            -   `2.3f`

    -   双精度

        -   使用`double`声明

        -   长 8 字节，保证 15 位十进制精度

        -   常量
            -   `2.3`

```c
#include <stdio.h>

int main(int argc, char *argv[]) {
    int oct = 0123;
    float fl = 12.3456789f;
    char character = 'a';

    printf("oct integer: %d\n", oct);
    printf("float: %f\n", fl);
    printf("character: %c\n", character);
    return 0;
}
```

    oct integer: 83
    float: 12.345679
    character: a

-   字元

    分为`signed`、`unsigned`即有、无符号两种，默认有

    -   使用`char`来声明

    -   占用 1 字节

    -   本质是 1 字节整型，对应 ASCII 表

    -   常量

        -   'a'

        -   转义序列

            -   `\\` \ 字符

            -   `\'` ' 字符

            -   `\"` " 字符

            -   `\?` ? 字符

            -   `\a` 警报铃声

            -   `\b` 退格键

            -   `\f` 换页符

            -   `\n` 换行符

            -   `\r` 回车

            -   `\t` 水平制表符

            -   `\v` 垂直制表符

            -   `\127` 一到三位的八进制数

            -   `\xAB1F4` 一个或多个数字的十六进制数

        -   通用字符名

            -   `\uACDF` 后四位为 Unicode 编码（不足四位在前自动补 0）

            -   `\uAC2FEE84` 后八位为 Unicode 编码（不足八位在前自动补 0）

-   指针

    -   使用 `*` 声明

    -   长 4 字节，本质为内存地址

    -   声明后若未初始化，则指向未知位置

## 数组

使用 `类型名称 名称[长度（可选）] = 数组常量;` 形式并初始化

-   数组常量形为 `{常量, 常量, 常量, 常量}`

-   数组的名称实为其首元素地址，但对其求 `sizeof` 时会返回**整个**数组大小

-   声明时若未手动初始化，则自动初始化为`0`的相应类型转换

-   内存中变现为连续地址，多维数组亦然

### 字符串

-   本质为`char`组成的数组，有`string.h`帮助操作
-   可以使用 `char 名称[长度（可选）] = 字符串常量` 来声明并初始化，使用`%s`来打印

-   声明时（如下例`name`变量）会自动在尾部追加`\0`

-   如果字符串末尾的`\0`缺失，代码将崩溃。

-   字符串声明时若未手动初始化，则自动初始化为`\0`

-   常量，

    -   `"Hello,world!"` ASCII-0 字符串

    -   `R"F:\Doc\1"` raw 字符串

    -   `u8"你好"` `u"你好"` `U"你好"` `L"你好"` 编码序列 UTF-8、char16_t、char32_t、wchar_t

    -   常量尾部会被自动添加`\0`

    -   相邻常量会被自动连接

#### 输出格式化

-   `%a` 浮点数、十六进制数字和 p-记数法（c99)
-   `%A` 浮点数、十六进制数字和 p-记法（c99）
-   `%c` 一个字符(char)
-   `%C` 一个 ISO 宽字符
-   `%d` 有符号十进制整数(int)（%ld、%Ld：长整型数据(long),%hd：输出短整形。）
-   `%e` 浮点数、e-科学记数法
-   `%E` 浮点数、E-科学记数法
-   `%f` 单精度浮点数(默认 float)、十进制记数法（%.nf 这里 n 表示精确到小数位后 n 位.十进制计数）
-   `%g` 根据数值不同自动选择%f 或%e．
-   `%G` 根据数值不同自动选择%f 或%e.
-   `%i` 有符号十进制数（与%d 相同）
-   `%o` 无符号八进制整数
-   `%p` 指针
-   `%s` 对应字符串 char\*（%s = %hs = %hS 输出 窄字符）
-   `%S` 对应宽字符串 WCAHR\*（%ws = %S 输出宽字符串）
-   `%u` 无符号十进制整数(unsigned int)
-   `%x` 使用十六进制数字 0xf 的无符号十六进制整数
-   `%X` 使用十六进制数字 0xf 的无符号十六进制整数
-   `%%` 打印一个百分号

```c
#include <stdio.h>

int main(int argc, char *argv[]) {
    int areas[] = {10, 12, 13, 14, 20};
    int numbers[5] = {5};
    char name[] = "Zed";
    char full_name[] = {
        'Z', 'e', 'd',
         ' ', 'A', '.', ' ',
         'S', 'h', 'a', 'w', '\0'
    };

    printf("%d\n", areas[0]);
    printf("%d %d %d %d\n", numbers[0], numbers[1], numbers[2], numbers[3]);
    printf("%c\n", name[2]);
    printf("%c\n", full_name[4]);
    return 0;
}
```

    10
    5 0 0 0
    d
    A

### `char a[] = "string";` 与 `char *p = "string";`

内存中：

```
     +---+---+---+---+---+---+----+
  a: | s | t | r | i | n | g | \0 |
     +---+---+---+---+---+---+----+
     +-----+     +---+---+---+---+---+---+---+
  p: |  *======> | s | t | r | i | n | g |\0 |
     +-----+     +---+---+---+---+---+---+---+
```

对于`p`其`string\0`为常量，不可修改，如果要创建可修改字符串，使用`*alloc()`

## 结构体

```C
struct Books {
   char  title[50];
   char  author[50];
   char  subject[100];
   int   book_id;
}
```

1. 使用 `.` 访问

```python
#include <stdio.h>

struct Book {
   int id;
} bok; // 立即声明 bok 为 结构体

int main(int argc, char *argv[]) {
    bok.id = 1;
    printf("%d", bok.id);
    return 0;
}
```

2. 使用 `->` 访问

    `a->b` 等同 `(*a).b`

```python
#include <stdio.h>
#include <stdlib.h>

// 使用 typedef 取别名
typedef struct Book {
    int id;
} Book;

int main(int argc, char *argv[]) {
    Book *bok; // 声明一个指向结构体的指针；此处因指针未初始化，代码实际不可用
    bok->id = 12;
    (*bok.)id = 12;
    return 0;
}
```

### 复杂声明

```python
char *(*(*var)())[10];
// ^ ^ ^ ^ ^ ^ ^^   ^
// 7 6 4 2 1 2 34   5
```

从变量标识符开始，向右寻找最近的`)`或`]`并解释，向左寻找`*`并解释，重复直至结束：

1. var 被声明为

2. 指向以下的指针

3. 返回以下的函数

4. 指向以下的指针

5. 包含 10 个元素的数组，内容为

6. 指向以下的指针

7. char 值

总结：var 被声明为（指向（返回（指向（包含 10 个元素的数组，内容为（指向（char 值）的指针）的指针）的函数）的指针）

> var 内容为 地址 --> 函数返回：地址 --> 数组内容：地址 --> char 值

## 存储类

-   auto

    局部，默认

-   register

    存储于寄存器

-   static

    静态，一经声明不再销毁

-   extern

    外部，用于多文件调用

-   typedef

    声明别名，例：

```python
#include <stdio.h>
typedef int integer;
integer a = 11;

int main() {
    printf("%d\n", a);
    return 0;
}
```

    11

## 类型限定

-   const

    定义为常量。

-   volatile

    则该对象可以被其他进程或事件修改。

## 类型转换

C 语言为隐式转换，显式强制转换使用 `(void *)name` 表达式
