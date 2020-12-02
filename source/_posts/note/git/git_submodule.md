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
permalink: /note/git/submodule
hidden: true
---

# git 子模块

[回到笔记目录](/note/git/index)

当在一个 repo 中使用了另外一个 repo 时，应使用 submodule

<!-- more -->

在子模块中可以像使用普通 repo 一样进行编辑、提交、拉取或推送，**但是应预先于子模块文件夹中`git checkout <commit-ish>`或`switch`以确保在编辑正确的分支**

-   `git submodule [--quiet] status [--cached] [--recursive] [--] [<path>…​]`

    列出 `path` 子模块，如不指定则全数列出，`status`可以省略

-   `git submodule [--quiet] add [<options>] [--] <repository> [<path>]`

    将 `repository` 作为子模块添加到 `path`，会记录其`branch`及`commit`号，并以此分离`submodule`的 HEAD

-   `git submodule [--quiet] update [--remote ] [--checkout|--rebase|--merge [<options>] [--] [<path>…​]`

    更新 `path` 子模块到记录的`branch`及`commit`号

    -   `--remote` 不再使用记录的`branch`及`commit`号而使用`submodule`**上游版本库**的

    -   `--checkout` 更新记录的`branch`及`commit`号，并以此分离`submodule`的 HEAD

    -   `--merge` 记录的`branch`及`commit`号会被`merge`到`submodule`的当前分支

    -   `--rebase` 记录的`branch`及`commit`号会被`rebase`到`submodule`的当前分支

    综上，

    如果要切换子模块的`commit`，则`cd`进入然后`checkout`，

    如果想要切换子模块到其最新版本：`git submodule update --remote --merge`，当然也可以`cd`进入子模块然后`git pull`然后`checkout`

-   `git submodule [--quiet] init [--] [<path>…​]`

    若 `path` 子模块未加载，则使用此命令 `clone` 之

-   `git submodule [--quiet] deinit [-f|--force] (--all|[--] <path>…​)`

    删除 `path` 子模块

-   `git submodule [--quiet] set-branch [<options>] [--] <path>`

    `git submodule [--quiet] set-url [--] <path> <newurl>`

    编辑要使用的 `path` 子模块分支或项目地址
