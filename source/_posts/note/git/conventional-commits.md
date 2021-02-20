---
title: git commit 规范
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
permalink: /note/git/conventional-commits
hidden: true
---

[回到笔记目录](/note/git/index)

# git commit 规范

规范的 commit 有助于管理版本历史及自动化

> (https://www.conventionalcommits.org/)

<!--more-->

## 格式简述

一个 commit 的格式应为：

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

-   type 类型：

    1. `fix`: 修复（用于表示 `PATCH` [版本号](https://semver.org)）
    2. `feat`: 新功能（用于表示 `MINOR` [版本号](https://semver.org)）
    3. 在类型后紧跟 `!` 表示一个前向不兼容变更（用于表示 `MINOR` [版本号](https://semver.org)
    4. 其他类型，比如 [@commitlint/config-conventional](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional)（基于[Angular convention](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines)）中推荐使用的 `build:`、`chore:`、`ci:`、`docs:`、`style:`、`refactor:`、`perf:`、`test:`等

-   footer 脚注：

    1. `BREAKING CHANGE`: 当脚注中存在`BREAKING CHANGE: <description>`，表示一个前向不兼容变更（用于表示 `MINOR` [版本号](https://semver.org)，可以用于任何类型
    2. 其他脚注

-   作用域用于提供改变的位置 e.g. `feat(parser): add ability to parse arrays.`
