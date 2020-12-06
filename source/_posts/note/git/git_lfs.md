---
title: git 大文件
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
permalink: /note/git/lfs
hidden: true
---

# git 大文件

[回到笔记目录](/note/git/index)

git lfs 用于储存二进制文件

<!-- more -->

## 常用命令

-   `git lfs version`:
    版本号

---

-   `git lfs track <path>`:
    添加到 .gitattributes
-   `git lfs untrack <path>`:
    移除

---

-   `git lfs dedup`:
    删除重复 LFS 项

---

-   `git lfs push`:
    推送 LFS 项至上游
-   `git lfs fetch`:
    下载
-   `git lfs pull`:
    下载并`checkout`相应版本

---

-   `git lfs install`:
    全局安装 LFS
-   `git lfs uninstall`:
    全局卸除 LFS

---

-   `git lfs lock`:
    锁定一个文件
-   `git lfs unlock`:
    解锁
-   `git lfs locks`:
    查看锁定

-   `git lfs migrate`:
    将项目转移至 LFS

---

-   `git lfs status`:
    查看工作树中 LFS 项状态
-   `git lfs ls-files`:
    查看工作树及暂存区中 LFS 项状态

## 简单工作流

1.  全局安装:
    ```sh
    git lfs install
    ```
2.  添加文件:
    ```sh
    git lfs track "*.iso"
    ```
3.  暂存`.gitattributes`:
    ```sh
    git add .gitattributes
    ```
4.  提交:
    ```sh
    git add file.iso
    git commit -m "Add disk image"
    git push
    ```

## .lfsconfig

[文档](https://github.com/git-lfs/git-lfs/blob/master/docs/man/git-lfs-config.5.ronn)
