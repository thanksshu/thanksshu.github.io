---
title: PHP 语句
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
permalink: /note/php/statement
---

# 语句

[回到笔记索引](/note/php/index)

## Declare

```PHP

declare (directive)
    statement

```

-   ticks

    Tick（时钟周期）是一个在 declare 代码段中解释器每执行 N 条可计时的低级语句就会发生的事件

    ```PHP

    <?php
    // these are the same:

    // you can use this:
    declare(ticks=1) {
        // entire script here
    }

    // or you can use this:
    declare(ticks=1);
    // entire script here
    ?>

    ```

-   encoding

    可以用 encoding 指令来对每段脚本指定其编码方式

    ```PHP

    <?php
    declare(encoding='ISO-8859-1');
    // code here
    ?>

    ```

## For 一家

```PHP

for (expr1; expr2; expr3)
    statement

```

亦可：

```PHP

for (expr1; expr2; expr3):
    statement;
    ...
endfor;

```

foreach 数组对象遍历专业户：

```PHP

foreach (array_expression as $value) // 获取值
    statement

foreach (array_expression as $key => $value) //获取值与键
    statement

```

当 foreach 开始执行时，数组内部的指针会自动指向第一个单元

## If 一家

可以（花括号在内部单句时不必要）：

```PHP

<?php
if ($a > $b) {
    echo "a is bigger than b";
} elseif ($a == $b) {
    echo "a is equal to b";
} else {
    echo "a is smaller than b";
}
?>

```

还可以：

```PHP

<?php
if ($a > $b):
    echo "a is bigger than b";
else if ($a == $b):
    echo "a is equal to b";
else:
    echo "a is smaller than b";
endif;
?>

```

## Switch

执行 `==` 比较而不是 `===` ：

```PHP

<?php
switch ($i) {
    case 0: // 会落到下一个判断
    case 1:
        echo "i equals 1";
        break;
    case 2:
        echo "i equals 2";
        break;
    default: // 没有匹配的话：
        echo "i is not equal to 0, 1 or 2";
}
?>

```

另一种：

```PHP

<?php
switch ($i):
    case 0:
        echo "i equals 0";
        break;
    case 1:
        echo "i equals 1";
        break;
    case 2:
        echo "i equals 2";
        break;
    default:
        echo "i is not equal to 0, 1 or 2";
endswitch;
?>

```

## While 一家

while:

```PHP

while (expr) {
    statement
}

```

还可以：

```PHP

while (expr):
    statement
    ...
endwhile;

```

do...while，do 内至少执行一遍:

```PHP

<?php
$i = 0;
do {
   echo $i;
} while ($i > 0);
?>

```

## 错误处理

```PHP
try {
    throw new Exception('Division by zero.'); // 需要捕获错误的部分
} catch (Exception $e) {
    echo $e; // 出现相应错误时运行（这里打印了错误），然后便跳出
} finally {
    // 无论如何都执行
}
```
