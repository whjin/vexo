---
title: Vue基础教程
date: 2019-02-18 23:34:23
category: ["技术"]
tags: ["前端","Vue"]
---

开发工具准备：

1. 根据个人喜欢选择`IDE`，我使用的是`WebStorm`，推荐使用`Atom`和`VSCode`；
2. 安装`git base`和`node.js`；
3. 安装`vue-cli`，命令`npm i -g @vue/cli`；
4. 新建`vue-cli`项目：
    1. 方法一：通过图形界面进行安装`vue ui`；
    2. 方法二：通过命令行安装`vue create project-name`
5. 运行项目`npm run serve`，端口`8080`。

<!--more-->

## 双向绑定v-model ##

双向绑定大多用于表单事件，通过监听使用者输入的事件来更新内容。

现阶段大部分工作在`App.vue`上，`template`与普通写法一致，`js`写法：

```javascript
export default {
    name: 'app',
    data() {
        return {
            title: 'vue.js',
            myname: '请输入名字'
        }
    }
}
```

## 去掉空白符.trim ##

直接在`v-model`后加上`.trim`即可。

```html
<input type="text" v-model.trim="name" value="name">
```

## 懒加载.lazy ##

在离开`input`时才更新输入的内容，在`v-model`后加上`.lazy`即可。

## 限定输入数字.number ##

在`v-model`后加上`.number`即可。

## 遍历v-for ##

遍历有一个基本的模板：

```html
<div id="app">
    <ul v-for="(item,index) in member" :key="index">
        <li>{{item}}</li>
    </ul>
</div>
```

## 组件component ##

在`App.vue`中引入`components`中的组件：

```javascript
<template>
  <div id="app">
    <Card />
  </div>
</template>

<script>
  import Card from './components/Card'
  
  export default {
    components: {
      Card
    }
  }
</script>
```

## 数据传递props ##

```html
<template>
    <div id="app">
        <Card :cardData="cardData"/>
    </div>
</template>
```

其中`:cardData="cardData"`是这个组件的核心，用于绑定属性`cardData`。其他数据展示工作放在`Card.vue`组件中进行。

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="js" data-user="whjin" data-slug-hash="darQdg" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="props接收数据">
  <span>See the Pen <a href="https://codepen.io/whjin/pen/darQdg/">
  props接收数据</a> by whjin (<a href="https://codepen.io/whjin">@whjin</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

这里解析一下`<div class="card_wall"></div>`包裹`<div class="card"></div>`主要是方便后期应用扩展，以及让应用整体更稳定。

## 生命周期 ##

我不喜欢用官网的生命流程图来讲解这个内容，使用文字表达更加让思维清晰。

1. **初始化**：设置数据监听，编译模板，挂载到`DOM`并在数据变化时更新`DOM`等；
2. 生命周期钩子：其实就是一个过程处理，类似于服务站。

**生命周期钩子简介**

1. `beforeCreate`：实例初始化
2. `created`：实例建立完成（可以取得`$data`）
3. `beforeMount`：模板挂载之前（还没有生成`html`）
4. `mounted`：模板挂载完成
5. `beforeUpdate`：如果`data`发生变化，触发组件更新，重新渲染
6. `updated`：更新完成
7. `beforeDestroy`：实例销毁之前（实例还可以使用）
8. `destroyed`：实例已销毁（所有绑定被解除、所有事件监听器被移除、所有子实例被移除）

生命周期钩子用得最多的是`mounted`，主要用在调用属性、方法的时候，

## 指令 ##

### v-once指令 ###

第一次渲染完成后变为静态内容，其下的所有子元素都是这样的效果。

### v-pre指令 ###

`v-pre`指令会让指定元素被忽略。

### v-cloak指令 ###

`v-cloak`指令用于去除页面渲染数据时出现闪现的情况，使用方法：

```html
<template>
  <div id="app">
    <div v-cloak>${ item.title }</div>
  </div>
</template>

<style>
  [v-cloak] {
      display: none;
  }
</style>
```

### v-html指令 ###

`v-html`指令会把`html`标签渲染成`DOM`显示在页面上。

`v-html`指令只能对可信任的用户使用，否则容易受到`XSS`攻击。

## 动画 ##

**Vue**动画一般在真正需要使用的情况下才加入页面，推荐在**CSS**中使用动画。

### 加入渐变的时机 ###

1. `v-if`条件渲染
2. `v-show`条件显示
3. 动态组件
4. 组件的根节点

### 渐变的分类 ###

1. `v-enter`定义**进入渐变**时**开始**的样式。
    - 只存在组件插入前，组件插入后就移除。
2. `v-enter-active`定义**进入渐变**的**过程**效果，可以设定渐变过程的时间（`duration`）和速度曲线（`easing curve`）。
    - 在组件被插入前生效，在完成动画时移除。
3. `v-enter-to`定义**进入渐变**后**结束**的样式。
    - 在组件被插入后生效，同时`v-enter`被移除，并在完成**进入渐变**动画时移除。
4. `v-leave`定义**离开渐变**时**开始**的样式。
    - 在触发组件**离开渐变**时生效，接着马上移除。
5. `v-leave-active`定义**离开渐变**的**过程**效果，可以设定渐变过程的时间（`duration`）和速度曲线（`easing curve`）。
    - 在触发组件**离开渐变**时生效，在完成动画时移除。
6. `v-leave-to`定义**离开渐变**后**结束**的样式。
    - 在触发组件**离开渐变**时生效，同时`v-enter`被移除，并在完成**离开渐变**动画时移除。

![](https://vuejs.org/images/transition.png)

### transition自定义名称 ###

```html
<template>
  <div id="app">
    <div class="main">
      <button @click="change = !change">縮放控制器</button>
      <transition name="zoom">
        <div v-if="change" class="ant_man_style"></div>
      </transition>
    </div>
  </div>
</template>
```

```css
.zoom-enter, .zoom-leave-to {
width: 0px;
height: 0px;
}
.zoom-enter-active, .zoom-leave-active {
transition: width 1s, height 1s;
}
```

### animation ###

可以使用CSS中的`animation`动画设计更为华丽的效果。

```css
.zoom-leave-active {
animation: special_effects 1.5s;
}

.zoom-enter-active {
animation: special_effects 1.5s reverse;
}

@keyframes special_effects {}
```

### transition自定义动画类别 ###

除了在`<transition>`中设定`name`自定义前缀（属性），还可以预设动画类别。

- `enter-class`定义进入动画时**开始**的样式。
- `enter-active-class`定义进入动画的**过程**效果。
- `enter-to-class`定义进入动画后**结束**的样式。
- `leave-class`定义离开动画时**开始**的样式。
- `leave-active-class`定义离开动画的**过程**效果。
- `leave-to-class`定义离开动画后**结束**的样式。

以上六个自定义属性**优先级别**高于一般渐变类别。

> CSS动画库：[Animation.css](https://daneden.github.io/animate.css/)

### JavaScript钩子 ###

`<transition>`还可以绑定JavaScriptHooks，除了单独使用，也能结合CSS `transition`和`animations`一起使用。

- `beforeEnter(el)`在**进入渐变或动画**前生效。
- `enter(el,callback)`在**进入渐变或动画**的组件插入时生效。
- `afterEnter(el)`在**进入渐变或动画**结束时生效。
- `enterCanceled(el)`在**未完成渐变或动画**时取消。
- `beforeLeave(el)`在**离开渐变或动画**前生效。
- `leaveCancelled(el)`在**未完成渐变或动画**时取消。

```html
<transition
  @before-enter="beforeEnter"
  @enter="enter"
  @after-enter="afterEnter"
  @enter-cancelled="enterCancelled"
  @before-leave="beforeLeave"
  @leave="leave"
  @after-leave="afterLeave"
  @leave-cancelled="leaveCancelled">
  <div v-if="change" class="ant_man_style"></div>
</transition>
```

在`enter`和`leave`中必须使用`done`，不然它们会同时生效，动画也会瞬间完成。

### 设定初始载入时的渐变 ###

如果想要设定一开始载入画面时组件的渐变效果，可以通过设定`appear`属性来实现。

- `appear-class`载入时**开始**的样式。
- `appear-to-class`载入**过程**的样式。
- `appear-active-class`载入**结束**时样式。

```html
<transition
        appear
        appear-class="show-appear-class"
        appear-to-class="show-appear-to-class"
        appear-active-class="show-appear-active-class">
</transition>
```

先在`<transition>`标签内加入`appear`，接着类似自定义动画可以给`class name`命名。

### 初始载入JavaScript Hooks ###

- `beforeAppear`载入前
- `appear`载入时
- `afterAppear`载入后
- `appearCancelled`取消载入（载入开始后）

```html
<div id="app">
  <transition
    appear
    @before-appear="beforeAppear"
    @appear="appear"
    @after-appear="afterAppear"
    @appear-cancelled="appearCancelled">
    <div v-if="change" class="ant_man_style"></div>
  </transition>
</div>
```

### key ###

对相同的标签元素使用`key`进行区分。

### 渐变模式in-out和out-in ###

#### in-out模式 ####

1. 新加入的元素做渐变进入。
2. 渐变进入结束后，原存在的元素再渐变离开。

#### out-in模式 ####

1. 原存在的元素渐变离开。
2. 渐变离开结束后，新元素再渐变进入。

```html
<transition mode="out-in"></transition>
<transition mode="in-out"></transition>
```

### 列表过渡 ###

- `<transition-group>`会渲染出一个`html`标签，预设是`<span>`，也可以选择自定义`tag`为其他标签。
- 无法使用（渐变模式`in-out`和`out-in`），因为不再是元素之间来回切换。
- 每个元素需要设定一个`key`值，不能重复。

### 列表乱数排序 ###

`<transition-group>`能够改变数组的排序，使用前需要先安装`shuffle`

```javascript
npm i --save lodash.shuffle

let shuffle = require('lodash.shuffle')
```

## 过滤器filter ##

### `filters`串联 ###

`filter`可以同时串联多个`filter`函数。

### filters参数 ###

## $emit ##

1. 父组件可以使用`props`把数据传递给子组件。
2. 子组件可以使用`$emit`触发父组件的自定义事件。





