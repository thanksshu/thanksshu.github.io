---
title: python 笔记
layout: post
comments: true
tags:
    - python
categories:
    - - 笔记
      - python
hidden: false
date: 2020-11-27 12:40:00
updated:
permalink: note/python
---

# Python 笔记

## 装饰器

-   接受函数作为参数并返回函数的函数

```python
def decorator(func):
    def warpper(*args, **kwargs):
        do_something()
        return func(*args, **kwargs)
    return warpper

@decorator
function(*args, **kwargs):
    pass
```

<!--more-->

`@decorator`语法糖在执行时，将`function`传入`decorator`，打包为`warpper`并将`warpper`返回为新`function`，此时`function`已经是`warpper`——被装饰过的了

-   接受参数的装饰器

```python
def decorator_factory(argument):
    def decorator(function):
        def wrapper(*args, **kwargs):
            funny_stuff()
            something_with_argument(argument)
            result = function(*args, **kwargs)
            more_funny_stuff()
            return result
        return wrapper
    return decorator

@decorator_factory(arg)
function(*args, **kwargs):
    pass
```

## 闭包

-   保存作用域

```python
def genClosure(time = 0):
    _time = time
    def closure(delta: int):
    nonlocal _time
    _time += delta
    print(_time)
    return _time
    return closure

timer = genClosure()
timer(1)
timer(1)
timer(1)
timer(1)
```

-   无闭包

```python
fs = []
for i in range(5):
def f():
return i
fs.append(f)

for j in fs:
print(j())
```

## 变量机制

python 全体变量可视为引用传值

### 标识、相等性和别名

1. 赋值：创建一个对象并让变量指向它

```python
 a = 255657
 b = 255657
 print(f'a的地址：{id(a)} b的地址：{id(b)}')
 print(f'a 是 b 吗？{a is b}')

```

    a的地址：139923749274576 b的地址：139923749273808
    a 是 b 吗？False

3. 内存驻留：复用常见的对象以优化内存使用

```python
 a = 1
 b = 1
 print(f'a的地址：{id(a)} b的地址：{id(b)}')
 print(f'a 是 b 吗？{a is b}')
```

    a的地址：9435456 b的地址：9435456
    a 是 b 吗？True

2. 引用：让另一个变量指向同一位置

```python
 a = 255657
 b = a
 print(f'a的地址：{id(a)} b的地址：{id(b)}')
 print(f'a 是 b 吗？{a is b}')

```

    a的地址：139923749274032 b的地址：139923749274032
    a 是 b 吗？True

3. 函数传参：由于是引用传参，可变对象会被函数修改

```python
def f(list):
    list.pop()

l = [1, 2, 3]
print(l)

f(l)

print(l)

```

    [1, 2, 3]
    [1, 2]

```python
## 一个形似闭包的例子
def f(list=[]):
    list.append('element')
    return list

print(f())
print(f())
print(f())
print(f())

```

    ['element']
    ['element', 'element']
    ['element', 'element', 'element']
    ['element', 'element', 'element', 'element']

### 可变与不可变类型

-   不可变类型：一经创建无法改变，通过创建新对象获取新值

    -   int

    -   float

    -   decimal

    -   complex

    -   bool

    -   string

    -   tuple

    -   range

    -   frozenset

    -   bytes

-   可变类型

    -   list

    -   dict

    -   set

    -   bytearray

    -   user-defined classes (unless specifically made immutable)

### 简单与容器（container）类型

-   容器类型：用于存放对象的类型

    -   list 列表
    -   set 集合
    -   tuple 元组
    -   dict 字典

-   简单类型：容器类型之外的
