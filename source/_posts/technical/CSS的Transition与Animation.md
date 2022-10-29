---
title: CSS的Transition与Animation
date: 2019-05-08 17:40:49
category: ["前端","CSS"]
tags: ["CSS"]
comments:
---

> 本文总结CSS3中两个用来做动画的属性，一个是`transition`，另一个是`animation`。

<!--more-->

# 差异比较 #

|CSS3|差异|
|----|----|
|`transition`|在给定的持续时间内平滑地更改属性值（从一个值到另一个值），也就是只需要指定开始与结束的参数，参数改变时就触发动画。|
||常用语鼠标事件（`:hover`、`active`、`:focus`、`:click`）或键盘输入时触发|
||需要事件触发，无法在网页加载时自动发生。一次性，不能重复发生，除非一再触发。|
||只能定义开始状态和结束状态，不能定义中间状态。|
|`animation`|可以自行写动画开始、进行间、结束时各阶段的变化，适合用来做较细微的动画表现。需要明确的指定关键帧（`@keyframe`）的参数。|
||网页加载时会直接执行，可以自行控制各阶段动画的变化|

> `animation`和`transition`最大的不同在于`transition`是当参数改变时触发，而`animation`则是直接就执行，所有动画效果需要明确的指定关键帧的参数。

|CSS3|简写顺序|
|----|-------|
|`transition`|[`property`名称][`duration`时间][`timing-function`特效][`delay`延迟]|
|`animation`|[`name`名称][`duration`时间][`timing-function`特效][`delay`延迟]|
||[`iteration-count`次数][`direction`方向][`fill-mode`填充模式][`play-state`播放状态]|

# 浏览器支持 #

## `transition`写法 ##

```css
.box {
  width: 100px;
  height: 100px;
  background-color: purple;
  transition: width 2s ease-in 2s;
}

.box:hover {
  width: 200px;
  height: 200px;
  background-color: red;
}
```

## `animation`写法 ##

```css
.box {
  width: 100px;
  height: 100px;
  border: 1px solid #ccc;
  animation: change 5s; /*8个属性中至少要有名称、时间*/
}

/*设定开始与结束状态*/
/*from 就是0%，to 就是100%*/
@keyframes change {
  from {
    background-color: #4BC0C8;
  }
  to {
    background-color: #C779D0;
  }
}
```

```css
.box {
  width: 100px;
  height: 100px;
  border: 1px solid #ccc;
  animation: change 5s; /*8个属性中至少要有名称、时间*/
}

/*设定开始与结束状态*/
/*from 就是0%，to 就是100%*/
@keyframes change {
  0% {
    background-color: #4BC0C8;
  }
  20% {
    background-color: #C779D0;
  }
  60% {
    background-color: #FEAC5E;
  }
  80% {
    background-color: #185a9d;
  }
  100% {
    background-color: #4BC0C8;
  }
}
```

|属性|值|
|----|---|
|`animation-name`|`@keyframes`后的名称|
|`animation-duration`时间|`time`以秒计算，如`3s initial`预设值`inherit`继承父层|
|`animation-timing-function`特效|`linear`等速、`ease`、`ease-in`、`ease-out`、`ease-in-out`、`step-start`、`step-end`、`steps(int,start/end)`、`cubic-bezier(n,n,n,n)`[可上官网取值使用](https://cubic-bezier.com/#.17,.67,.83,.67)|
|`animation-delay`|以秒计算，如`2s`|
|`animation-iteration-count`次数|`number`预设值为`1`，因此填`2`时，动画跑的次数为`1+2=3`次`infinite`无限循环|
|`animation-direction`方向|`normal`、`reverse`反向、`alternate`先反后正|
|`animation-fill-mode`|`forwards`使用关键帧最后的值`backwards`使用最开始的值`both`|
|`animation-play-state`播放状态|`pause`暂停`running`为预设值`initial`预设值、`inherit`继承父层|

## `Animation.css` ##

官网下载：[Animate.css](https://daneden.github.io/animate.css/)
GitHub：[Animate.css 使用说明](https://github.com/daneden/animate.css)

