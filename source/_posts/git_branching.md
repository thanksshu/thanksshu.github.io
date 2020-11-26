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
permalink:
---

# git 分支

包含 `branch` `switch` `merge` `rebase` `cherry-pick` 等

<!-- more -->

[LearnGitBranching](https://learngitbranching.js.org/?locale=zh_CN)

-   `branch` 显示所有分支

    -   `<新分支名>` 创建新分支 -`<commit or HEAD^>` 指定从 commit 创建分支
    -   `-d <分支名>` 删除分支
    -   `-D <分支名>` 强行删除分支

-   `switch <分支名>` 切换到分支

-   `merge <commit 或 分支>` 合并分支
    -   `--no-commit` 只合并不提交
-   `mergetool` 在 merge 后调用文本编辑工具进行比对选择
-   `rebase <upstream>` rebase 分支
    -   `-i` 交互式 rebase
-   `cherry-pick <commit>` cherry-pick 分支
