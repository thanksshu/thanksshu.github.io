---
title: git 子模块
layout: post
comments: true
tags:
    - 版本管理
    - git
categories:
    - 笔记
    - Git
date: 2020-11-26 12:00:00
updated:
permalink:
---

# git 子模块

当在一个 repo 中使用了另外一个 repo 时，应使用 submodule

<!-- more -->

在子模块中可以像使用普通 repo 一样进行编辑、提交、拉取或推送，**但是应预先于子模块文件夹中`git switch <子模块分支>`以确保在编辑正确的分支**

1. `git submodule [--quiet] status [--cached] [--recursive] [--] [<path>…​]`

    列出 path 子模块，如不指定 path 则全数列出，可以省略 status

2. `git submodule [--quiet] add [<options>] [--] <repository> [<path>]`

    将 repository 作为子模块添加到 path

3. `git submodule [--quiet] update [<options>] [--] [<path>…​]`

    更新 path 子模块

4. `git submodule [--quiet] init [--] [<path>…​]`

    若 path 子模块未加载，则使用此命令 clone 之

5. `git submodule [--quiet] deinit [-f|--force] (--all|[--] <path>…​)`

    删除 path 子模块

6. `git submodule [--quiet] set-branch [<options>] [--] <path>`

    `git submodule [--quiet] set-url [--] <path> <newurl>`

    编辑要使用的 path 子模块分支即项目地址
