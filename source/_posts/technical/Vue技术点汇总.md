---
title: Vue技术点汇总
date: 2023-01-22 16:57:15
category: ["前端","技术"]
tags: ["Vue","JavaScript"]
---

### 响应式数据 ###

根据数据类型【数组和对象】进行不同处理。

1. 对象内部通过`defineReactive`方法，使用`Object.defineProperty()`监听数据属性的`get`进行数据依赖收集，再通过`set`完成数据更新。

2. 数组则通过重写数组方法实现。扩展`7`个变更方法（`push/pop/shift/unshift/splice/reverse/sort`），通过监听这些方法收集依赖和派发更新。

> 多层对象通过递归实现监听，`Vue3`使用`proxy`实现响应式数据。
> 响应式流程：`defineReactive`定义响应式数据；给属性增加`dep`收集对应的`watcher`；等数据变化进行更新。
> `dep.depend`——`get`取值，依赖收集；`dep.notify`——`set`设置，通知视图更新。

<!--more-->

性能优化点：1. 对象层级过深；2. 不需要响应式数据不放在`data`；3. `Object.freeze`可以冻结数据。

