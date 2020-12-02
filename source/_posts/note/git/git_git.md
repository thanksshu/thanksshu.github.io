---
title: git 概念
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
permalink: /note/git/basic
hidden: true
---

# git 概念

[回到笔记目录](/note/git/index)

1. [官网](https://git-scm.com/)

2. [cheatsheet](https://ndpsoftware.com/git-cheatsheet.html)

3. [内置环境变量](https://git-scm.com/book/en/v2/Git-Internals-Environment-Variables)

<!-- more -->

## 基本概念 [手册链接](https://git-scm.com/docs/gitglossary.html)

### 命令

- git 命令行使用 '--' 来分隔版本和路径

### 存储区

git 主要有：

-   工作区 worktree: 是直接编辑的地方
-   暂存区 index: 数据暂时存放的区域
-   本地版本库 local repository: 存放已经提交的数据
-   上游版本库 upstream repository: 存放已经提交并推送的数据
-   存档库 stash: 暂时存放数据的堆栈

### 常用名词

-   `origin`：默认上游版本库

-   `master`：默认本地版本库分支

-   `pathspec`：git 用于指定文件、路径的格式

---

-   [`object`](https://git-scm.com/book/en/v2/Git-Internals-Git-Objects)：git 的存储单位，每一个都被唯一`SHA-1`值所标记，分为`commit`、`tree`、`tag`和`blob`四种，一般存储在`.git/objects/`

-   [`ref`](https://git-scm.com/book/en/v2/Git-Internals-Git-References)：以`refs/`开头的名称（e.g. `refs/heads/master`），指向一个`object`或另一个`ref`；存储在`.git/refs/`中

-   [`refspec`](https://git-scm.com/book/en/v2/Git-Internals-The-Refspec)：描述 local 与 remote 间的映射关系，

    如格式：`<src>:<dst>`，其中`<src>`与`:`可以省略，例见[push](/note/git/remote#推送)

---

-   `head` 或 `head ref`：分支顶的`ref`，存储于`.git/refs/heads/`

-   `HEAD` 或 `@`：当前分支，(关于`@`)[https://mirrors.edge.kernel.org/pub/software/scm/git/docs/gitrevisions.html]

-   `commit` ：同`commit object`

-   `tree`：工作区 或 `tree object`——一个等效于目录（`directory`）的`object`

-   `commit-ish` 与 `tree-ish`：用于表示一个`commit object`或`tree object`的`object`

    一些例子：

    ```
    ----------------------------------------------------------------------
    |    commit-ish/tree-ish    |                examples
    ----------------------------------------------------------------------
    |  1. <sha1>                | dae86e1950b1277e545cee180551750029cfe735
    |  2. <describe_output>     | v1.7.4.2-679-g3bee7fb
    |  3. <refname>             | master, heads/master, refs/heads/master
    |  4. <refname>@{<date>}    | master@{yesterday}, HEAD@{5 minutes ago}
    |  5. <refname>@{<n>}       | master@{1}
    |  6. @{<n>}                | @{1}
    |  7. @{-<n>}               | @{-1}
    |  8. <refname>@{upstream}  | master@{upstream}, @{u}
    |  9. <rev>^                | HEAD^, v1.5.1^0
    | 10. <rev>~<n>             | master~3
    | 11. <rev>^{<type>}        | v0.99.8^{commit}
    | 12. <rev>^{}              | v0.99.8^{}
    | 13. <rev>^{/<text>}       | HEAD^{/fix nasty bug}
    | 14. :/<text>              | :/fix nasty bug
    ----------------------------------------------------------------------
    |       tree-ish only       |                examples
    ----------------------------------------------------------------------
    | 15. <rev>:<path>          | HEAD:README.txt, master:sub-directory/
    ----------------------------------------------------------------------
    |         tree-ish?         |                examples
    ----------------------------------------------------------------------
    | 16. :<n>:<path>           | :0:README, :README
    ----------------------------------------------------------------------
    ```

-   `checkout`：以某个`object`为参照更新工作区（更换`HEAD`位置到新分支）
