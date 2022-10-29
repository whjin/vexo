---
title: 读书笔记-Web安全一
date: 2019-02-23 05:17:37
category: ["前端"]
tags: ["Web安全","黑客"]
comments:
---

这是一个系列笔记，来自**《Web前端黑客技术揭秘》**这本书，属于进阶内容，可以进一步提高Web开发的能力。

<!--more-->

# Web安全的关键点 #

## 数据和指令 ##

1. SQL注入攻击

`selct username,email,desc from users where id=1`

攻击者提交：

`union select password,1,1 from users`

最终SQL查询语句：

`selct username,email,desc from users where id=1 union select password,1,1 from users`

组成的SQL语句合法，通过一个经典的`union`查询，此时注入的指令内容就会被当做合法指令执行。这样的攻击会导致`users`表中的`password`泄露。

2. XSS跨站脚本攻击

`eval`函数能够动态执行`url`返回的特定信息，比如`eval(location.hash.substr(1))`即是截取`#`后的`callback`内容，提供给`eval`进行动态执行。

如果攻击者对`#`后的`url`中的`#`后的内容进行改造，就可以截取到访问者的`cookies`会话信息，其中可能包含访问者的账号、密码等重要信息。

> SQL注入攻击针对的对象是数据库，大多发生在服务端，或者说是存储端，因为HTML5技术中有客户端存储技术。
> 跨站攻击主要发生在浏览器客户端。

## 浏览器的同源策略 ##

1. 不同域或同域名

同域要求两个站点同协议、同域名、同端口。

2. 客户端脚本

3. 授权

HTML5标准中默认不允许跨域访问，只有目标站点明确返回HTTP响应头。此时，站点上的客户端就有权通过Ajax技术对目标站点上的数据进行读写操作。

4. 读写权限

5. 资源

一般来说，资源包括：HTTP消息头、DOM树、浏览器存储。

# 前端基础 #

## URL ##

URL有个重点就是编码方式，有三类：`escape`、`encodeURI`、`encodeURIComponent`，对应的解码函数是：`unescape`、`decodeURI`、`decodeURIComponent`。

## HTTP协议 ##

URL的请求协议几乎都是HTTP，它是一种无状态的请求相应，即每次的请求相应之后，连接会立即断开或延时断开（保持一定的连接有效期），断开后，下一次请求再重新建立。

HTTP是无状态的，每次在连接时，服务端通过`cookies`进行会话跟踪，第一次响应时设置的`cookies`在随后的每次请求中都会发送出去。`cookies`还可以包含登录认证后的身份信息。

每个`Set-Cookie`都设置一个`Cookie`（`key=value`）。

- `expires`：过期时间。
- `path`：相对路径，只有在这个路径下的资源可以访问这个`cookie`。
- `domain`：域名，有权限设置为更高一级的域名。
- `HTTPOnly`：标志（默认无，如果有，表明`cookie`存在于HTTP层面，不能被客户端脚本读取）。
- `Secure`：标志（默认无，如果有，表明`cookie`仅通过HTTPS协议进行安全传输）。

## JavaScript跨站 ##

### DOM树操作 ###

1. 获取HTML内容中的隐私数据

2. 获取浏览器的`cookies`数据

3. 获取URL地址中的数据

### AJAX风险 ###

Ajax严格遵守同源策略，既不能从另一个域读取数据，也不能发送数据到另一个域。

**CORS方案**

来源域的Ajax向目标域发起了请求，浏览器会自动带上Origin头，然后目标域要判断这个Origin值，如果是预期的，就返回：

`Access-Control-Allow-Origin: http://www.foo.com`

表示同意跨域。

### 模拟用户发起浏览器请求 ###

