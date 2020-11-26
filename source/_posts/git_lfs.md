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
permalink:
---

# git 大文件

git lfs 用于储存二进制文件

<!-- more -->

## 常用命令

-   `git lfs version`:
    Report the version number.

---

-   `git lfs track <path>`:
    View or add Git LFS paths to Git attributes.
-   `git lfs untrack <path>`:
    Remove Git LFS paths from Git Attributes.

---

-   `git lfs dedup`:
    De-duplicate Git LFS files.

---

-   `git lfs push`:
    Push queued large files to the Git LFS endpoint.
-   `git lfs fetch`:
    Download Git LFS files from a remote.
-   `git lfs pull`:
    Fetch Git LFS changes from the remote & checkout any required working tree
    files.

---

-   `git lfs install`:
    Install Git LFS configuration.
-   `git lfs uninstall`:
    Uninstall Git LFS by removing hooks and smudge/clean filter configuration.

---

-   `git lfs lock`:
    Set a file as "locked" on the Git LFS server.
-   `git lfs unlock`:
    Remove "locked" setting for a file on the Git LFS server.
-   `git lfs locks`:
    List currently "locked" files from the Git LFS server.

-   `git lfs migrate`:
    Migrate history to or from Git LFS

---

-   `git lfs status`:
    Show the status of Git LFS files in the working tree.
-   `git lfs ls-files`:
    Show information about Git LFS files in the index and working tree.

## Examples

To get started with Git LFS, the following commands can be used.

1.  Setup Git LFS on your system. You only have to do this once per
    repository per machine:

        git lfs install

2.  Choose the type of files you want to track, for examples all ISO
    images, with git lfs track:

        git lfs track "*.iso"

3.  The above stores this information in gitattributes(5) files, so
    that file need to be added to the repository:

        git add .gitattributes

4.  Commit, push and work with the files normally:

        git add file.iso
        git commit -m "Add disk image"
        git push
