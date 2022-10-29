---
title: JavaScript知多少
date: 2018-11-13 07:57:49
category: ["前端"]
tags: ["javascript"]
---

# `this`与对象原型`prototype` #

# `hoisting`状态提升 #

在程序执行前，编译器先由上到下逐行将代码转为机器可读的命令，然后再执行编译后的指令。

> 实现一个函数，可以返回输入参数是否为质数？

<!--more-->

```javascript
function isPrimeNumber(m) {
    if (m <= 1 || m % 1 !== 0) {
        return false;
    }
    var n = 2;
    while (n < m) {
        if (m % n === 0) {
            return false;
        } else {
            n++;
            continue;
        }
    }
    return true;
}
```

> 实现一个函数，如果传入的参数是字符串，则将该字符串按照字母出现的次数由大到小重新排列并输出；如果传入的参数不是字符串，则将参数输出。

**分析：**

1. 首先，使用`for`循环找出相同的字母，此时需要知道字母出现的次数；
2. 然后，给它们进行排序`sort()`，但是`sort()`是数组方法；
3. 考虑把字符串先转换为数组，处理完毕之后再转换回字符串；
4. 使用`split()`（字符串方法，输出为数组），如果内容为空，则返回的是整个字符串作为数组的第一个元素且数组只包含这一个元素。如果`split`传入内容为`''`，即`split('')`，则字符串里的每个字符分别作为输出数组的元素；
5. 处理完毕需要再转换为字符串，使用`join()`（数组方法，输出位字符串），传入内容`join('')`；
6. 使用正则表达式查找重复字符。

> `classList.toggle(class,true/false)`

<p class="codepen" data-height="365" data-theme-id="0" data-default-tab="html,result" data-user="whjin" data-slug-hash="MRdePN" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="js-toggleMenu">
  <span>See the Pen <a href="https://codepen.io/whjin/pen/MRdePN/">
  js-toggleMenu</a> by whjin (<a href="https://codepen.io/whjin">@whjin</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

# 事件处理 #

```html
<span onmouseover="over(this)" onmouseout="out(this)">Test</span>
<div onmouseover="over(this)" onmouseout="out(this)">Line</div>
```

```javascript
function over(element) {
  element.style.color = 'red'
}

function out(element) {
  element.style.color = 'blue'
}
```

# `jsonp`实现代码 #

```javascript
function JSONP({
    url,
    params,
    callbackKey,
    callback
}) {
    // 在参数里制定callback的名字
    params = params || {}
    params[callbackKey] = 'jsonpCallback'
    // 预留callback
    window.jsonpCallback = callback
    // 拼接参数字符串
    const paramKeys = Object.keys(params)
    const paramString = paramKeys
        .map(key => `${key}=${params[key]}`)
        .join('&')
    // 插入DOM元素
    const script = document.createElement('script');
    script.setAttribute('src', `${url}?${paramString}`)
    document.body.appendChild(script)
}

JSON({
    url: "http://s.weibo.com/ajax/jsonp/suggestion",
    params: {
        key: 'test'
    },
    callbackKey: '_cb',
    callback(result) {
        console.log(result.data)
    }
})
```

# 实现防抖函数 #

防抖函数原理：在事件被触发`n`秒后再执行回调，如果在这`n`秒内又被触发，则重新计时。

```javascript
// 防抖函数
const debounce = (fn, delay) => {
    let timer = null;
    return (...args) => {
        clearTimeout(timer)
        timer = setTimeout(() => {
            fn.args(this, args)
        }, delay)
    }
}
```

适用场景：

- 按钮提交：防止多次提交按钮，只执行最后提交的一次
- 服务端验证：表单验证需要服务端配合，只执行一段连续的输入事件的最后一次，还有搜索联想词的功能类似

# 实现节流函数 #

节流函数原理：规定在一个单位时间内，只能触发一次函数。如果这个单位时间内触发多次函数，只有一次生效。  

```javascript
// 节流函数
const throttle = (fn, delay = 500) => {
    let flag = true;
    return (...args) => {
        if (!flag) return;
        setTimeout(() => {
            fn.apply(this, args)
            flag = true
        }, delay)
    }
}
```

适用场景：

- 拖拽：固定时间内只执行一次，防止超高频次触发位置变动
- 缩放场景：监控浏览器`resize`
- 动画：避免短时间内多次触发动画引起性能问题

# 深克隆 #

