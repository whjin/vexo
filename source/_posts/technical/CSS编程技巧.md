---
title: CSS-编程技巧
date: 2019-03-13 18:31:43
category: ["前端","CSS"]
tags: ["CSS"]
comments:
---

# CSS-编程技巧 #

- 使用百分比而不是固定的宽度。或者使用相对的宽度：`vw`, `vh`, `vmin`, `vmax`
- 在大屏幕上要有一个固定宽度的元素时，使用 `max-width`，让其不用`media query`就能自适应小屏幕
- 在 `img`, `object`, `video`, `iframe` 加上 `max-width: 100%`
- 当需要填充元素的背景图片时，使用 `background-size: cover` 让图片能保持原始比例。在移动设备上使用高解析图片不是明智的做法
- 制作 `grid` 页面时让 `viewport width` 来决定每一列的数量。`Flexbox` 或者 `display: inline-block` 就可以做到
- 当制作多栏的的文字区块时，设定 `column-width` 而不是 `column-count`，让你在小屏幕上会得到一个栏位

<!--more-->

**减少重复代码**原则：

## 半透明的边界 ##

<p class="codepen" data-height="365" data-theme-id="0" data-default-tab="result" data-user="whjin" data-slug-hash="QoaWPX" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="Secret 1: 半透明的边界">
  <span>See the Pen <a href="https://codepen.io/whjin/pen/QoaWPX/">
  Secret 1: 半透明的边界</a> by whjin (<a href="https://codepen.io/whjin">@whjin</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## 内部圆角 ##

<p class="codepen" data-height="365" data-theme-id="0" data-default-tab="result" data-user="whjin" data-slug-hash="JzMJRY" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="内部圆角">
  <span>See the Pen <a href="https://codepen.io/whjin/pen/JzMJRY/">
  内部圆角</a> by whjin (<a href="https://codepen.io/whjin">@whjin</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## 背景图案 ##

<p class="codepen" data-height="465" data-theme-id="0" data-default-tab="result" data-user="whjin" data-slug-hash="BbYaGV" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="背景图案">
  <span>See the Pen <a href="https://codepen.io/whjin/pen/BbYaGV/">
  背景图案</a> by whjin (<a href="https://codepen.io/whjin">@whjin</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## （伪）随机背景图案 ##

<p class="codepen" data-height="465" data-theme-id="0" data-default-tab="result" data-user="whjin" data-slug-hash="qvxEjP" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="（伪）随机背景图案">
  <span>See the Pen <a href="https://codepen.io/whjin/pen/qvxEjP/">
  （伪）随机背景图案</a> by whjin (<a href="https://codepen.io/whjin">@whjin</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## 不间断的图片边界 ##

<p class="codepen" data-height="465" data-theme-id="0" data-default-tab="result" data-user="whjin" data-slug-hash="EMQKvp" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="不间断的图片边界">
  <span>See the Pen <a href="https://codepen.io/whjin/pen/EMQKvp/">
  不间断的图片边界</a> by whjin (<a href="https://codepen.io/whjin">@whjin</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## 灵活的椭圆形 ##

<p class="codepen" data-height="365" data-theme-id="0" data-default-tab="result" data-user="whjin" data-slug-hash="eXVzzx" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="灵活的椭圆形">
  <span>See the Pen <a href="https://codepen.io/whjin/pen/eXVzzx/">
  灵活的椭圆形</a> by whjin (<a href="https://codepen.io/whjin">@whjin</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## 平行四边形 ##

<p class="codepen" data-height="465" data-theme-id="0" data-default-tab="result" data-user="whjin" data-slug-hash="qvoqbo" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="平行四边形">
  <span>See the Pen <a href="https://codepen.io/whjin/pen/qvoqbo/">
  平行四边形</a> by whjin (<a href="https://codepen.io/whjin">@whjin</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## 钻石形图片 ##