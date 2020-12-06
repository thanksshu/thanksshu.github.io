---
title: git 本地
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
permalink: /note/git/local
hidden: true
---

# git 本地

[回到笔记目录](/note/git/index)

包含 `init` `add` `tag` `reset` `restore` 等

<!-- more -->

-   `init` 创建空仓库

-   `add` 添加**工作区**改动到**暂存区**

    -   `-i` 进行交互式操作
    -   `-n` 预演，不真正添加
    -   `-f` 强行添加，能够添加被忽略文件

    ***

    -   ` .` 添加*更改、添加、删除*变动
    -   `-u` 添加全部*更改、删除*变动，无*添加*
    -   `--ignore-removal` 添加全部*更改、添加*变动，无*删除*

-   `rm` 在**暂存区**与**工作区**中删除文件

    -   `--cached` 仅从**暂存区**删除

-   `mv` 在**暂存区**与**工作区**中移动文件

-   `status` **工作区**相对**暂存区**状态变化

-   `diff` 对比**工作区**与**暂存区**或**本地版本库**

    -   `--cached <commit>` 对比**暂存区**与指定 commit
    -   `<commit 或 分支>` 对比**工作区**与指定 commit 或分支
    -   `<commit> <commit>` 对比两个 commit

-   `commit` 提交**暂存区**到**本地版本库**

    -   `--amend` 改写方才的提交
    -   `[-m 'msg']` 提交说明
    -   `-a` 自动添加**工作区**变动到**暂存区**并提交至版本库

-   `tag <tag> <commit>` 添加标签，此标签全局唯一
    `-d <tag>` 删除
    `-l` 列出全部
    `-m <msg>` 为标签添加信息
    `--file <file>` 从文件读取待添加信息
    `-e` 编辑消息

-   `rebase <commit-ish>` rebase commit
    -   `-i` 交互式 rebase，功能强大

## 恢复版本

[当项目有如一团乱麻时的建议](http://justinhileman.info/article/git-pretty/git-pretty.png)

> `<commit>` 相对位置举例：
>
> `HEAD^` 回到上一版本
>
> `HEAD^^^` 回到三个版本前
>
> `HEAD~10` 回到十个版本之前

-   `checkout <commit-ish>` *分离 HEAD*到某个 commit，不常用；其余使用情况复杂，不赘述

    > 如要恢复 HEAD，重新`switch`（见[分支](/note/git/branch)）到分支名即可

-   `revert <commit>` 以提交一个新 commit 的形式，抵销变动直至与指定 commit 一致，要求**工作区**与现在**本地版本库**最新 commit 一致

-   `reset` 将**本地版本库** HEAD 回滚至某个 commit:

    -   `--mixed <commit>` 保留**工作区**变动、撤销**暂存区**（默认）
    -   `--soft <commit>` 保留**工作区**变动、不撤销**暂存区**
    -   `--hard <commit>` 不保留**工作区**变动，撤销**暂存区**指定文件为最近一次**本地版本库**commit

        -   `<文件名>` 撤销指定文件为指定 commit

-   `restore <文件>` 丢弃未 commit 变动

    默认丢弃**工作区**变动，采用**暂存区**版本

    -   `--source=<tree>` 采用**本地版本库**的一个版本
    -   `--staged` 丢弃**暂存区**变动，采用**本地版本库**的一个版本
    -   `--worktree` 丢弃**工作区**变动，采用**本地版本库**的一个版本

## 查看版本

-   `log [<options>] [<revision range>] [[--] <path>…​]` 查看**本地版本库** commit 日志

    -   `-p` 详细模式
    -   `--graph` 使用树状图示
    -   `--all` 显示全部分支

    -   `--format=<format>` `<format>`可以为 `oneline`、`short`、`medium`（默认）、`full`、`fuller`、`reference`、`email`、`raw`、`format:<string>`、`tformat:<string>`
        - `<string>` 格式化format，详见官网
    -   `--oneline` 简化单个 commit 信息，为`--format`的一个简写

    ***

    -   `<revision range>`

        -   `<commit1>..<commit2>` 双点等同于 `^<commit1> <commit2>` 其中 `^` 代表不显示

        -   `<commit1>...<commit2>` 三点表示仅显示二者不同的部分（A...B == A..B + B..A）

-   `reflog` 本地操作历史，如果有时日不长的误操作，可从此撤销

-   `show <commit>` 查看单次 commit 详细历史

-   `grep <字符串>` 查找字符串
    -   `-c` 匹配数目
    -   `-n` 显示行号
