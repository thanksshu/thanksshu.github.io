---
title: CMake 简单使用
layout: post
comments: true
tags:
    - C
    - CMake
categories:
    - - 笔记
      - CMake
hidden: false
date: 2020-11-27 10:50:00
updated:
permalink: note/cmake
---

# CMake 简单使用

## [命令行](https://cmake.org/cmake/help/v3.19/manual/cmake.1.html)

```sh
生成构建系统
 cmake [<options>] <path-to-source>
 cmake [<options>] <path-to-existing-build>
 cmake [<options>] -S <path-to-source> -B <path-to-build>
```

-   `-D <var>:<type>=<value>` 设定变量
-   `-G <generator-name>` 指定生成器
-   `--graphviz=[file]` 生成依赖图
-   `-A <platform-name>` 指定平台

```sh
构建一个项目
 cmake --build <dir> [<options>] [-- <build-tool-options>]
```

<!--more-->

## [CMakeLists.txt](https://cmake.org/cmake/help/v3.19/manual/cmake-commands.7.html)

```
.
├── CMakeLists.txt
├── src
│   ├── a.c
│   └── b.c
└── include
    ├── a.h
    └── b.h
```

```cmake
cmake_minimum_required(VERSION 3.10)

# 项目名称
project(Tutorial)

# 生成目标
add_executable(Tutorial src/a.c src/b.c include/a.h include/b.h)

# 链接库
target_link_libraries(Tutorial PUBLIC m)

# 链接头文件
target_include_directories(Tutorial PUBLIC include/)
```

-   变量使用 `${...}` 访问

### 基本命令

命令存在作用域，一般会以前缀方式表示，尽量避免全局函数

#### 定义变量与属性

注意：变量是存在作用域的

-   定义变量

```cmake
set(<variable> <value>... [PARENT_SCOPE])
```

-   定义布尔变量

```cmake
option(<variable> "<help_text>" [value])
```

-   定义对象属性

```cmake
set_property(<GLOBAL                      |
              DIRECTORY [<dir>]           |
              TARGET    [<target1> ...]   |
              SOURCE    [<src1> ...]
                        [DIRECTORY <dirs> ...] |
                        [TARGET_DIRECTORY <targets> ...]
              INSTALL   [<file1> ...]     |
              TEST      [<test1> ...]     |
              CACHE     [<entry1> ...]    >
             [APPEND] [APPEND_STRING]
             PROPERTY <name> [<value1> ...])
```

#### file

1. 将 `<globbing-expr>` 匹配内容列表存储到 `<variable>` 中

```cmake
file(GLOB <variable>
     [LIST_DIRECTORIES true|false] [RELATIVE <path>] [CONFIGURE_DEPENDS]
     [<globbing-expressions>...])
file(GLOB_RECURSE <variable> [FOLLOW_SYMLINKS]
     [LIST_DIRECTORIES true|false] [RELATIVE <path>] [CONFIGURE_DEPENDS]
     [<globbing-expressions>...])
```

-   `CONFIGURE_DEPENDS` 会使编译工具在构建时重新读取`variable`

### 项目命令

只能在 CMake 项目内使用

#### project

1. 定义项目名及属性

```cmake
project(<PROJECT-NAME> [<language-name>...])

project(<PROJECT-NAME>
        [VERSION <major>[.<minor>[.<patch>[.<tweak>]]]]
        [DESCRIPTION <project-description-string>]
        [HOMEPAGE_URL <url-string>]
        [LANGUAGES <language-name>...])
```

#### 定义二进制目标（target）

1. 可执行文件

```cmake
add_executable(<name> [WIN32] [MACOSX_BUNDLE]
               [EXCLUDE_FROM_ALL]
               [source1] [source2 ...])
```
- `source` 应包含头文件

2. 库

```cmake
add_library(<name> [STATIC | SHARED | MODULE]
            [EXCLUDE_FROM_ALL]
            [<source>...])
```

#### target\_\*

e.g:

-   `target_include_directories()`：指定目标包含的头文件路径

-   `target_link_libraries()`：指定目标链接的库

-   `target_compile_options()`：指定目标的编译选项

以

```cmake
target_include_directories(<target>
  <INTERFACE|PUBLIC|PRIVATE> [items1...]
  [<INTERFACE|PUBLIC|PRIVATE> [items2...] ...])
```

为例：

-   `target`为`add_library`或`add_executable`创建

-   `PRIVATE`：私有，`item`仅对本级`c`文件可用，上级不可用

-   `INTERFACE`：接口，`item`对本级`h`文件可用，上级可用

-   `PUBLIC`：公有，等于前二者并集

### [变量](https://cmake.org/cmake/help/latest/manual/cmake-variables.7.html)

变量一般是全局的、cmake 预设或者用户定义的

-   `ENV{NAME}`: 环境变量，可`set`值

-   `CMAKE_BUILD_TYPE`：目标构建类型

-   `CMAKE_SYSTEM_NAME`：目标系统

-   `CMAKE_SYSTEM_PROCESSOR` 目标构架

-   `CMAKE_<LANG>_COMPILER` 指定语言编译器

-   `CMAKE_C_COMPILER_TARGET` 对支持指定编译目标的系统传入目标

-   `CMAKE_BINARY_DIR`、`PROJECT_BINARY_DIR`、`<projectname>_BINARY_DIR`：工程编译发生的目录

-   `CMAKE_SOURCE_DIR`、`PROJECT_SOURCE_DIR`、`<projectname>_SOURCE_DIR`: 工程顶层目录

-   `CMAKE_CURRENT_SOURCE_DIR`: 当前处理的 CMakeLists.txt 所在路径

-   `CMAKE_SYSTEM`：系统名称,比如 Linux-2.6.22

-   `CMAKE_SYSTEM_NAME`： 不包含版本的系统名,比如 Linux

-   `CMAKE_SYSTEM_VERSION`： 系统版本,比如 2.6.22

-   `CMAKE_SYSTEM_PROCESSOR`： 处理器名称,比如 i686.

### [属性](https://cmake.org/cmake/help/v3.19/manual/cmake-properties.7.html)

`GLOBAL`、`DIRECTORY`、`TARGET`等对象的属性

#### TARGET

-   `LIBRARY_OUTPUT_DIRECTORY` 库输出路径
-   `LIBRARY_OUTPUT_NAME` 库名称
-   `RUNTIME_OUTPUT_DIRECTORY` 最终二进制可执行文件输出目录
-   `RUNTIME_NAME_DIRECTORY` 可执行文件名称

-   `C_STANDARD` C 语言标准
-   `CXX_STANDARD` C++语言标准
