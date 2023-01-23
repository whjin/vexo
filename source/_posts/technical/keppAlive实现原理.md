---
title: kepp-alive实现原理
date: 2019-10-10 18:46:27
category: ["Vue"]
tags: ["Vue"]
comments: true
---

# `keep-alive`介绍 #

> `keep-alive`与`transition`相似，只是一个抽象组件，它不会在`DOM`树种渲染，也不在父组件链中存在。
> `keep-alive`是`Vue`的内置组件，能在组件切换过程中将状态保留在内存中，防止重复渲染`DOM`。
> 使用`keep-alive`包裹动态组件时，会缓存不活动的组件实例，而不是销毁它们。

<!--more-->
