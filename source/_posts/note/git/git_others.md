---
title: git 其余操作
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
permalink: /note/git/others
hidden: true
---

# git 设置及其余操作

[回到笔记目录](/note/git/index)

包含`config`、`.gitignore`、`别名`

<!-- more -->

## 设置

### gitconfig

-   `git config [<file-option>] [--type=<type>] [--show-origin] [--show-scope] [-z|--null] name [value [value_regex]]` 添加或设置变量

    `git config [可选参数同上] --get name [value_regex]` 查看变量

    `git config [<file-option>] --unset name [value_regex]` 删除变量

    `git config [<file-option>] -e | --edit` 打开设置文件以编辑

    ***

    -   `--local` 此工作区（默认）
    -   `--global` 用户全局
    -   `--system` 系统全局

_亦可使用`.gitconfig`文件设置_

#### 别名

```shell
git config --global alias.display "log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all"

git display
```

### gitignore

基本只要将文件名、路径遵循[相应格式](https://git-scm.com/docs/gitignore#_pattern_format)写进`.gitignore`文件即可

[文档](https://git-scm.com/docs/gitignore)
