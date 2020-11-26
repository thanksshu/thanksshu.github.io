---
title: git 分支
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
permalink: note/git/branch
hidden: true
---

# git 分支

[回到目录](/note/git)

包含 `branch` `switch` `merge` `rebase` `cherry-pick` 等

<!-- more -->

[LearnGitBranching](https://learngitbranching.js.org/?locale=zh_CN)

-   `branch` 显示所有分支

    -   `git branch [-f] <branchname> [<start-point>]` 创建新分支
        -   `start-point` 一个`commit-ish`，指定从何处创建分支
        -   `-f` 强制重置分支起点
    -   `git branch (-d | -D) [-r] <branchname>…​`
        -   `-d` 删除分支，此分支必需已被合并
        -   `-D`等于`-df` 强行删除分支，不论合并与否
    -   `git branch (-m | -M) [<oldbranch>] <newbranch>`
        -   `-m` 重命名分支，新名称不得重名
        -   `-D`或`-mf` 强行删除分支，不论重名与否
    -   `git branch (-c | -C) [<oldbranch>] <newbranch>`
        -   `-c` 复制分支，复制出的分支名称不得重名
        -   `-C`或`-cf` 强行删除分支，不论重名与否

-   `switch <分支名>` 切换到分支

-   `merge <commit 或 分支>` 合并分支
    -   `--no-commit` 只合并不提交
    -   `--allow-unrelated-histories` 允许合并无关的历史
-   `mergetool` 在 merge 后调用文本编辑工具进行比对选择
-   `rebase <upstream>` rebase 分支
    -   `-i` 交互式 rebase
-   `cherry-pick <commit>` cherry-pick 分支
