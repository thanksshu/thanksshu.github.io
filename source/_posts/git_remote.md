---
title: git 远程
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
permalink: note/git/remote
hidden: true
---

# git 远程

与上游版本库交流，包含 `remote` `clone` `push` `fetch`等

<!-- more -->

-   `remote`
    -   `add <代号> <路径>` 添加**上游版本库**，亦可添加如`/home/thanksshu/repo/.git`的**本地版本库**
    -   `rename <old> <new>` 重命名
    -   `remove <name>` 删除
    -   `get-url [--push] [--all] <name>`
    -   `set-url [--push] <name> <newurl> [<oldurl>]` 更换路径
        -   `--add [--push] <name> <newurl>` 添加路径
        -   `--delete [--push] <name> <url>` 删除路径
    -   `[-v | --verbose] show [-n] <name>…​` 列出远程
    -   `prune [-n | --dry-run] <name>…​` 从本地去除上游版本库不复存在的分支

## 拉取

-   `fetch <代号> <refspec>` 从**上游版本库**下载，关于`refspec`，见()
-   `pull <代号> <refspec>` `fetch`然后`git merge <refspec>`

## 推送

-   `clone <repo>` 自动创建空**本地版本库**、添加**上游版本库**并作`pull`
-   `push`
    -   `<代号> <branch>` 向**上游版本库**分支推送，若不存在此分支则新建
    -   `<代号> <branch>:<branch>` **上游版本库**分支与**本地版本库**分支名称不同的推送
    -   `<代号> :<branch>` 向**上游版本库**分支推送空白
