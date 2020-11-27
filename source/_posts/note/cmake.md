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

```cmake
cmake_minimum_required(VERSION 3.10)

# 项目名称
project(Tutorial)

# 生成目标
add_executable(Tutorial tutorial.c tuto.c)

# 链接库
target_link_libraries(Tutorial PUBLIC m)

# 链接头文件
target_include_directories(Tutorial PUBLIC tuto.h)
```

-   变量使用 `${...}` 访问

### 基本命令

#### set

```cmake
set(<variable> <value>... [PARENT_SCOPE])
```

#### file

```cmake
file({GLOB | GLOB_RECURSE} <out-var> [...] [<globbing-expr>...])
```

将 `<globbing-expr>` 匹配内容列表存储到 `<out-var>` 中

### 项目命令

#### project

```cmake
project(<PROJECT-NAME> [<language-name>...])

project(<PROJECT-NAME>
        [VERSION <major>[.<minor>[.<patch>[.<tweak>]]]]
        [DESCRIPTION <project-description-string>]
        [HOMEPAGE_URL <url-string>]
        [LANGUAGES <language-name>...])
```

Supported languages include C, CXX (i.e. C++), CUDA, OBJC (i.e. Objective-C), OBJCXX, Fortran, ISPC, and ASM. By default C and CXX are enabled if no language options are given. Specify language NONE, or use the LANGUAGES keyword and list no languages, to skip enabling any languages.

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

### [常用变量](https://cmake.org/cmake/help/latest/manual/cmake-variables.7.html)

-   `EXECUTABLE_OUTPUT_PATH`、`LIBRARY_OUTPUT_PATH`：最终编译结果的二进制执行文件、库文件的存放目录，可`set`值

-   `CMAKE_BUILD_TYPE`：目标构建类型，可`set`值：`Debug`，`Release`，`RelWithDebInfo`，`MinSizeRel`等

-   `CMAKE_SYSTEM_NAME`：目标系统，可`set`值：`uname -s`返回值等

-   `CMAKE_SYSTEM_PROCESSOR` 目标构架，可`set`值：`uname -m`返回值等

-   `CMAKE_<LANG>_COMPILER` 指定语言编译器，可`set`值：编译器路径

-   `CMAKE_C_COMPILER_TARGET` 对支持指定编译目标的系统传入目标，例：对于 clang 编译器`set(CMAKE_C_COMPILER_TARGET arm-linux-gnueabihf)`

-   `ENV{NAME}`: 环境变量，可`set`值

-   `CMAKE_BINARY_DIR`、`PROJECT_BINARY_DIR`、`<projectname>\_BINARY_DIR`：工程编译发生的目录
-   `CMAKE_SOURCE_DIR`、`PROJECT_SOURCE_DIR`、`<projectname>\_SOURCE_DIR`: 工程顶层目录

-   `CMAKE_CURRENT_SOURCE_DIR`: 当前处理的 CMakeLists.txt 所在路径

-   `CMAKE_SYSTEM`：系统名称,比如 Linux-2.6.22

-   `CMAKE_SYSTEM_NAME`： 不包含版本的系统名,比如 Linux

-   `CMAKE_SYSTEM_VERSION`： 系统版本,比如 2.6.22

-   `CMAKE_SYSTEM_PROCESSOR`： 处理器名称,比如 i686.

-   `UNIX`： 在所有的类 UNIX 平台为 TRUE,包括 OS X 和 cygwin

-   `WIN32：在所有`的 win32 平台为 TRUE,包括 cygwin
