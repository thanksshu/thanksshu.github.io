---
title: git 多工作区
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
permalink: note/git/worktree
hidden: true
---

# git worktree

git 允许多个工作区同时存在，同时对多个分支进行编辑维护

<!-- more -->

-   `git worktree list [--porcelain]` 打印所有工作区信息

-   `git worktree add [-f] [--detach] [--checkout] [--lock] [-b <new-branch>] <path> [<commit-ish>]` 添加一个工作区，注意路径要在原工作区外
-   `git worktree remove [-f] <worktree>` 删除工作区
-   `git worktree move <worktree> <new-path>` 移动工作区（手动移动会出错）
-   `git worktree repair [<path>…​]` 修复工作区文件（手动移动出错后）

-   `git worktree prune [-n] [-v] [--expire <expire>]` 自动删除无用工作区

-   `git worktree lock [--reason <string>] <worktree>` 锁定以防止被 prune
-   `git worktree unlock <worktree>` 解锁
