---
title: 软件构架
layout: post
comments: true
tags:
    - mvc
    - mvp
    - mvvm
categories:
    - 笔记
hidden: false
date: 2020-11-27 13:10:00
updated:
permalink: note/architectural-pattern
---

# 软件构架

## MVC

Model–view–controller

-   Model：数据模型，用来存储数据

-   View：视图界面，用来展示 UI 界面和响应用户交互

-   Controller：控制器，监听模型数据的改变和控制视图行为、处理用户交互

View 指示 Controller 执行业务，Controller 修改 Model，Model 通知 View 更新，操作均为单向

## MVP

Model-view-presneter

切断的 View 和 Model 的联系，Presenter（原 Controller）作为中间桥梁

## MVVM

Model–view–viewmodel

Presenter 的位置被换为 ViewModel，与 View 内容直接双向绑定，无需手动更新
