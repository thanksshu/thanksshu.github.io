---
title: git 存储库
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
permalink: note/git/stash
hidden: true
---

# git 存储库

[回到目录](/note/git)

stash 储存暂存区和工作区改动至存储库，然后丢弃暂存区和工作区变动

<!-- more -->

-   `stash push [msg]` 保存当前**暂存区**到新的存档库，并且执行 git reset ‑‑hard 来回滚
-   `stash pop <stash>` 应用指定存档中的改动并删除；默认是最近的存档
-   `stash apply <stash>`从某个存档中将改变应用到**工作区**；默认是最近的存档
-   `stash list` 显示当前你有的所有存档
-   `stash show` 显示存档中记录的改动，对比存档生成时的原来状态；默认显示最后一个
-   `stash drop` 从存储区中删除单个存档；不指定 stash 则删除最后一个
-   `stash clear` 清空存档库
