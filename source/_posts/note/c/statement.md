---
title: C 语句
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
permalink: /note/c/statement
---

# 语句

[笔记索引](/note/c/index)

## break continue 与 return

省略

## do-while

<!--more-->

```python
#include <stdio.h>

int x = 3;
int y;

void main() {
    do
    {
        y = printf("%d\n",x);
        x--;
    } while ( x > 0 );
}
```

    3
    2
    1

## for

```c
for(INITIALIZER; TEST; INCREMENTER) {
    CODE;
}
```

-   INIT 初始化循环体
-   TEST 判断是否结束
-   CODE 在`TEST`返回`1`时执行
-   INCR 在 CODE 结束后执行

```python
#include <stdio.h>

int main()
{
   for (int i = 0; i < 5; i++)
   {
    printf("for %d\n",i);
   }
   return 0;
}
```

    for 0
    for 1
    for 2
    for 3
    for 4

## goto

```python
#include <stdio.h>

int main() {
    printf("0");
    printf("1");

    goto three;

    printf("2");

    three: printf("3");

    printf("4");
    printf("\n");
    return 0;
}
```

    0134

## if

亦可不使用大括号，仅用缩进。

```python
#include <stdio.h>

int main() {
    int x = 1;
    if (x == 1) {
        printf("1\n");
    } else if (x == 0) {
        printf("0\n");
    } else {
        ;
    }
    return 0;
}
```

    1

## null 语句

`;` 什么也不做

## switch case

```python
#include <stdio.h>

int main(){
    char c = 'c';
    switch(c)
    {
        case 'a' :
        case 'b' :
        case 'c' :
            break;
        case 'd' :
        case 'e' :
        case 'f' :
            printf("%c\n",c);
    }
    return 0;
}
```

## while

```python
#include <stdio.h>

int main() {
    int i = 10;
    while ( i >= 0 ) {
        printf("%d ",i);
        i--;
    }
    printf("\n");
    return 0;
}
```

    10 9 8 7 6 5 4 3 2 1 0
