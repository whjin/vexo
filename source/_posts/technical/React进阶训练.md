---
title: React进阶训练
date: 2019-04-17 21:13:13
category: ["前端"]
tags: ["React"]
comments:
---

# `redux` #

**`Redux`就是给JavaScript应用程序一个可以预测`state`的容器。**

<!--more-->

使用Redux的时候一定要记得以下三大原则：

1. `single source of truth`：应用程序的`state`，皆存储在唯一一个树状结构的`store`中；
2. `state is read-only`：唯一改变`state`的方式，发送一个描述如何改变的`action`；
3. `changes are made with pure functions`：为了描述`action`如何改变`state`，`reducer`必须改成`pure function`。

**具体运行**

1. 当我们要改`state`时，必须**通过`dispatch`发送一个`action`对象到`store`**，这个`action`对象是用来描述发生了什么事。
2. `store`基本上也不知道收到这个用来做什么，因为它是用来存储`state tree`的地方，所以`store`会**把「自己目前的`state`」及「`action`」交给给`Reducer`处理**。
3. `reducer`是一个`pure function`，它会**根据我们`action`的要求去做`state`的更改，并将新的`state`回传给`store`**。
4. 我们可以让`component`去做监听`redux`裡面的`storestate`，只要一旦发现`state`有发生变化，就会立即帮我们重新`Render`。

# `store` #

`store`主要的功能就是掌管应用程式的状态，并且有这些任务：

1. 掌管应用程式的状态
2. 用`getState()`读取`state`
3. 用`dispatch(action)`来更新`state`
4. 用`subscribe(listener)`注册`listener`
5. 利用`subscribe(listener)`回传的`function`注销`listener`

在`redux`的应用程式中，`store`只会有一个。

创建`state`的方法就是利用`createStore(reducer)`的方式创建它，而要发送`action`则利用`dispatch(action)`来达到，当`store`收到`action`时，则会调用`reducer`来帮忙更新`state`。


