---
title: PHP 命名空间
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
permalink: note/php/namespace
---

# 命名空间 （PHP 5.3）

[回到笔记索引](note/php/index)

类（包括抽象类和 traits）、接口、函数和常量 收到到命名空间影响，

---

-   `namespace` 必须在其它所有代码之前（包括 HTML、除了 `declare`）声明命名空间：

```PHP
<?php
namespace MyProject;

const CONNECT_OK = 1;
class Connection { /* ... */ }
function connect() { /* ... */  }

?>

```

---

`namespace MyProject\Sub\Level` 定义了子命名空间。

---

```PHP
<?php
namespace MyProject {

const CONNECT_OK = 1;
class Connection { /* ... */ }
function connect() { /* ... */  }
}

namespace { // 全局命名空间
session_start();
$a = MyProject\connect();
echo MyProject\Connection::start();
}
?>
```

多个命名空间使用大括号区分

---

使用时类似文件系统：

```PHP
/* 非限定名称 */
foo(); // 解析为 Foo\Bar\ foo，相对路径

/* 限定名称 */
subnamespace\foo(); // 解析为函数 Foo\Bar\ subnamespace\foo，相对路径

/* 完全限定名称 */
\Foo\Bar\foo(); // 解析为函数 Foo\Bar\foo，绝对路径
```

-   访问任意全局类、函数或常量，都可以使用完全限定名称

-   动态访问时必须使用使用完全限定名称，前导反斜杠不必要

-   如果当前命名空间中不存在该函数或常量，PHP 会退而使用全局空间中的函数或常量

[具体使用](https://www.php.net/manual/zh/language.namespaces.basics.php)

```PHP
use My\Full\Classname as Another, My\Full\NSname; // 多个引用

// (PHP 5.6)
use function My\Full\functionName;
use function My\Full\functionName as func;
use const My\Full\CONSTANT;
```

可以引入命名空间并给予别名，必须为完全限定，前导不推荐
