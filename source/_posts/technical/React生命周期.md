---
title: React生命周期
date: 2019-05-13 22:57:12
category: ["前端","框架","React"]
tags: ["React","生命周期"]
comments:
---

# React component lifecycle 生命周期 #

`React`的生命周期是`component`在建立和渲染的过程，以`component class`出发，`React`会做以下的过程：

<!--more-->

依照`component`被挂入DOM的过程分类，过程中会依序执行`component`的函数如下：

- `Mounting`：`component`被建立实体（即`react element`）后，渲染到DOM的过程：
    1. `constructor()`
    2. `static getDerivedStateFromProps()`
    3. `render()`
    4. `componentDidMount()`

- `Updating`：当`component`收到新的`props`时，更新状态（`state`），再重新渲染到DOM的过程：
    1. `static getDerivedStateFromProps()`
    2. `shouldComponentUpdate()`
    3. `render()`
    4. `getSnapshotBeforeUpdate()`
    5. `componentDidUpdate()`

- `Unmounting`：当`component`不被使用，从DOM移除的过程
    1. `componentWillUnmounted()`

- `Error Handling`：当`component`错误发生时
    1. `componentDidCatch()`