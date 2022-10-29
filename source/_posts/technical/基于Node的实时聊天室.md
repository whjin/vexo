---
title: 基于Node.js的实时聊天室
date: 2018-10-02 19:54:18
category: ["前端"]
tags: ["前端","后端"]
---

> **项目需求：**      
> 1、用`nodejs`的`socket.io`写了一个简易版的聊天室（**实时推送技术，无刷新实现信息实时更新，应用于在线聊天室、在线客服系统、评论系统和WebIM等**）      
> 
> 2、根据`socket.io`库给出的`api`以及《`nodejs`实战》给出的`demo`实现了, 也只是很基础的, 但放到服务器上后会有网络延迟, 顺序不正确等问题    
>   
> 3、看过网上的资料, 没看到有解释很全或者投入生产环境的代码, 都是一些`demo`
> 
> **想请教前辈, 对于一个业务开发中常用的聊天室模块:**
> 
> 1、应该如何去思考呢?
> 2、整个过程会涉及到哪些知识点?
> 3、会有哪些难点呢?(比如支持高并发啥的)
> 4、应该注意什么呢?(比如如何测试或者啥的?)

<!--more-->

# 解决方案 #

## 需求分析： ##

1. 实现在线聊天室的基本功能，包括显示在线用户的个人信息
2. 用户进行实时聊天，信息推送实时更新
3. 其他可扩展功能

![](https://i.imgur.com/6eGgAmr.png)

## 技术栈分析 ##

`socket.io`是一个开源`WebSocket`库，它通过`Node.js`实现`WebSocket`服务端，同时提供客户端`JS`库。`socket.io`支持以事件为基础的实时双向通讯，可以工作在任何平台、浏览器或移动设备。

1. `Node.js+Express/koa/egg`环境搭建
2. `socket.io`
3. 聊天基础版（壳模型）
4. 模板引擎（`jade/pug`）
5. 聊天界面
6. 系统消息
7. 用户上下线
8. 单聊和群聊
9. 图片发送
10. 功能完善
11. 项目总结


1. 首先需要先从一个产品的角度进行考虑：
	1. 设计草图，画出聊天室的大致样子，各个组件的位置，标注功能；
	2. 对每个组件进行分析，确认需要使用的技术；
	3. 再次确认细节，进行切图工作，如果不具备这项能力可以自己动手画图；
2. 搭建开发环境：
	1. 技术栈`Node.js+socket.io+Express/koa+Mongodb`；
	2. 安装`Node.js`并配置相关依赖，Express有自己的生成器
	3. 搭建壳模型，也就是最简易的聊天室
	4. 开发平台推荐使用Linux或者使用Mac
3. 功能介绍：
    1. 用户列表
        1. 用户登录
        2. 在线用户列表
    2. 文本消息传输
        1. 用户（谁发的消息）
        2. 时间（什么时候发的）
        3. 内容（发的什么内容）
    3. 图片传输
    4. 上下线通知
4. 技术点：
    1. `Node.js`
    2. `Express`
    3. `socket.io`（包括客户端和服务器端代码，这个直接看官网的文档）
        1. `server`
        2. `client`
    4. `html/css`
    5. `sco.js、messenger.js`
    6. **模板引擎（`jade/pug`）是非常重要的一个工具，配合`Node.js`可以帮助你完成一些复杂的任务，需要重点掌握**
    7. 聊天界面设计：
        1. 用户列表（用户上线添加/下线移除，用户每次的变更都进行整体更新，不做单独的移除。如果需要进行单独移除，可通过用户下线时的指定对象来移除特定用户）
        2. 聊天窗口
            1. 内容展示区（当前用户消息展示/对方用户消息展示）
            2. 消息发送区（图片传输功能键/消息输入区/消息发送功能键）
            3. 用户上下线通知
            4. 键盘事件
    8. 系统消息
        1. 界面提醒（上/下线提醒）
        2. `sco.js/message.js`    
    9. 用户上下线
![](https://i.imgur.com/EfROll6.png)

4. 具体实例可参考网上的资料：
    1. [Socket.io在线聊天室](http://blog.fens.me/nodejs-socketio-chat/)
    2. [bsspirit/chat-websocket](https://github.com/bsspirit/chat-websocket)
    3. [yinxin630/fiora](https://github.com/yinxin630/fiora)
    4. [lufeng501/nchat](https://github.com/lufeng501/nchat)
    5. [maochunguang/free_chat](https://github.com/maochunguang/free_chat)
    6. [一个WebSocket实时聊天室Demo：基于node.js+socket.io](http://www.52im.net/thread-516-1-1.html)
    7. [Node.js websocket 使用 socket.io库实现实时聊天室](https://blog.csdn.net/haodawang/article/details/56011749)
    8. [Node.js + Web Socket 打造即时聊天程序](https://zhuanlan.zhihu.com/p/36602333)
    9. [实战WebSocket聊天室：从开发到部署上线](http://www.rxshc.com/164.html)

## 项目总结 ##

1. 聊天室分为客户端和服务端，完整的应用其实就是把这两个模块连接起来实现数据通信，然后在分别对两个模块进行细分；
2. 根据细节的结果确定其中涉及的技术问题，逐一进行解决，类似于搭积木游戏；
3. 比如客户端模块需要`html/css/js`、模板引擎；服务器模块需要`Node.js/Express/Koa`、`sco.js/message.js`、数据库技术等；
4. `Node.js`很适合应用在高并发的场景中，高并发的场景可以使用Nginx来做负载均衡，会有哪些难点需要在实际项目中才会知道，大概是在读写数据和数据传输方面会有一些需要重点解决的问题；
5. 在`Node.js`中写测试，包括了测试框架、测试异步函数、私有方法、模拟测试环境、依赖`HTTP`协议的`web`应用，需要了解`TDD`和`BDD`，还有需要提供测试的覆盖率

### `Node.js`单元测试工具 ###

1. 测试框架：`mocha`
2. 断言库：`should.js`、`expect.js`、`chai`
3. 覆盖率：`istanbul`、`jscover`、`blanket`
4. Mock库：`muk`
5. 测试私有方法：`rewire`
6. Web测试：`supertest`
7. 持续集成：`Travis-cli`