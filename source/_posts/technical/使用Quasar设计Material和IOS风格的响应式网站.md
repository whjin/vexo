---
title: 使用Quasar设计Material和IOS风格的响应式网站
date: 2019-02-23 18:37:28
category: ["技术"]
tags: ["前端","Quasar"]
---

# Quasar #

`Quasar`是一款基于`Vue.js`开发的`UI`框架，可以让你轻松构建网站简洁明快的界面，更重要的是它还能让你轻松做好`RWD`（响应式网站设计），除此之外还能帮助你加上`PWA`，使你的网页变成手机上的`App`。

<!--more-->

以下内容来自官网[Quasar Framework](http://www.quasarchs.com/)，概括了`Quasar`的主要特点。

`Quasar`是`MIT`许可的开源框架（基于[Vue](https://cn.vuejs.org/)），可帮助`Web`开发人员创建：

- 响应式网站
- `PWA`
- 通过`Apache Cordova`构建移动`App`
- 多平台桌面应用程序（使用`Electron`）

## 选择Quasar的5个理由 ##

1. 内建了`Material`及`IOS`两种主题
2. 组件均内建`RWD`快速响应
3. 多样的基础`UI`组件库
4. 自带了`Vuex`、`VueRouter`、`Vuei18n`（多国语系）
5. 强大的部署工具

## 安装指南 ##

首先安装`Node.js`和`vue-cli`，具体安装方法查看官网资料。

然后安装`Quasar`，`npm install -g quasar-cli`。

最后搭建项目：`quasar init <folder name>`

取代`main.js`的`quasar.config.js`设置文件：

- 引用Quasar内建的组件，可以不用在每个地方`import components`
- `i18n`设置多国语系
- `icons`移除注释即可使用
- `开发模式`下的HTTPS以及`port`设置
- `CSS`动画设置
- 其他外部插件的设置
- `PWA`、`manifest`等设置

### quasar.config.js ###

- `plugins`

以前在`Vue`安装其他的`plugin`会在`main.js`里引入，而在`Quasar`就会取代`main.js`成为全部配置文件。

- `css`

CSS的引入都会放在这个文件，默认的位置`/src/css`，所需的CSS库已经准备好，可以直接使用。

- `extra`

这里是设置是否引入[quasar-extras](https://github.com/quasarframework/quasar-extras)的内容。

|Package|name|说明|
|-------|----|----|
|Roboto Font|`roboto-font`|Material主题的建议字体|
|Roboto Font Latin Extended|`roboto-font-latin-ext`|Material主题的建议字体|
|[Material Icons](https://material.io/tools/icons/?style=baseline)|`material-icons`|Material风格的`icon`|
|MDI (Material Design Icons)|`mdi`|Material风格的`icon`扩展|
|Font Awesome|`fontawesome`|自由选择`icon`|
|[Ionicons](https://ionicons.com/)|`ionicons`|`ionicons`的`icon`|
|Animate.css|`animations`|网页组件动画|

- `scopeHoiting`

默认`true`，用来提升`webpack`运行时的性能

- `VueRouterMode`

设置`Vue Router`的模式，有`history`、`hash`两种值。

- `vueCompiler`

包含两种Vue的编译模式`vue runtime`+`compiler`，默认只有`runtime-only`运行时编译

- `gzip`

使网站支持`gzip`的格式。

- `analyze`

在`build`时会运行`webpack-bundle-analyzer`工具。

![](https://d1dwq032kyr03c.cloudfront.net/upload/images/20181017/20111805z6Qs0mgwUv.png)

- `extractCSS`

提取CSS到文件中。[VueLoader](https://vue-loader-v14.vuejs.org/zh-cn/configurations/extract-css.html)

- `extendWebpack`

在`dev`模式中服务器的设置。


- `https`

- `port`

设置成指定的`port`，当quasar在运行`dev`模式时，遇到相同的`port`时会自己再`+1`。

- `open`

是否在`dev`指令执行完成后，自动开启此网站的分页在浏览器上。

### Layout ###

`quasar dev`打开初始页面，页面的`header`和`drawer`都是在`layout/MyLayout.vue`里。

![](https://ithelp.ithome.com.tw/upload/images/20181018/20111805omoWvkNkQj.png)

一些常用的属性：

|属性|取值|说明|
|---|---|----|
|`side`|`String`|有两个值`left`，`right`，决定要出现在左边还是右边|
|`overlay`|`Boolean`|设置侧边栏弹出时是挤压`q-page-container`还是直接盖在上面|
|`content-style`|`Object`|设置侧边栏的CSS|
|`content-class`|`String/Object/Array`|设置侧边栏的`class`|
|`mini`|`Boolean`|把侧边栏缩小到只有`icon`|

> 这里的CSS要用`Object`的方式传入。

```html
:content-style="{color: 'red'}"
```

## 旅游网站-Header ##

**演示项目：**

- Toolbar
- ToolbarTitle
- Button

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="html" data-user="whjin" data-slug-hash="MLNxZN" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="旅游网站-Header">
  <span>See the Pen <a href="https://codepen.io/whjin/pen/MLNxZN/">
  旅游网站-Header</a> by whjin (<a href="https://codepen.io/whjin">@whjin</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

### Toolbar ###

- `color`

Quasar内建色：[color-palette](http://www.quasarchs.com/components/color-palette.html)

在`/src/css/themes/common.variables.styl`里面增加调色板的颜色。

- `inverted`

让**背景色**变成**白色**，然后使原来白色的文字变成设置的**背景色**。

- `glossy`

加上玻璃效果

### QToolbarTitle ###

- `gt-xs`

用来设置显示像素高于`576px`的页面样式。

- `q-mr-md`

`mr`等于`margin-right`
`sm`就是`size`的值为`small`

![](https://ithelp.ithome.com.tw/upload/images/20181019/20111805O7e642RHjY.png)

**其他非外观的功能属性：**

- `disable`，`:disable="true"`时按钮禁用
- `label`设置按钮的文字
- `type`可以是`button`、`submit`、`reset`其中一种
- `loading`，值为`true`显示读取中
- `percentage`显示读取的圆圈，要跟`loading`一起使用
- `dark-percentage`用在亮色系的按钮上

### List&ListItem ###

**修改Drawer**

- `v-model="rightDrawerOpen"`控制弹出侧边栏的位置
- `content-class="bg-grey-10"`背景色
- `side="right"`按钮设置在多边

设置了`rightDrawerOpen`需要加到`data`里。

```javascript
export default {
  name: 'MyLayout',
  data () {
    return {
      rightDrawerOpen: false
    }
  }
}
```

### 手机端按钮 ###

控制显示的`class`用`lt-sm`只要像素小于`sm(768px)`就会显示该区域。

### 设置List和ListItem ###

**使用Dark属性使得组件内容在暗色背景下更好显示**

List中可用组件，这些组件需要自己去配置文件中自行引入。

- `QListHeader`List上的标题
- `QItemSeparator`分割线
- `QItem`
- `QItemSide`可分成左右两侧的区块
- `QItemMain`中间的区块
- `QItemTitle`区块中的标题

## 旅游网站-Carousel页面轮播 ##

### 建立新的首页 ###

在`src/pages/`下新建`Index`文件夹，并在此文件夹下新建`Index.vue`作为首页，删除原来的`Index.vue`文件。

### 修改Vue Router ###

在`src/router/routers.js`修改`Index.vue`的路径。

### 建立轮播的区块 ###

在`src/pages/Index`下新建`SectionCarousel.vue`，并在`Index.vue`中引入。

然后再`template`下的`q-page`中加入`section-carousel`

```html
<template>
  <q-page>
    <section-carousel></section-carousel>
  </q-page>
</template>
```

### 开始写轮播 ###

[官方Carousel](http://www.quasarchs.com/components/carousel.html)

在设置文件`quasa.config.js`中引入：

```javascript
framework: {
  components: [
    'QCarousel',
    'QCarouselSlide',
    'QCarouselControl'
    ...
  ],
}
```

### 加入轮播的图片/页面 ###

```html
<template>
  <q-carousel
    color="white"
    infinite
    arrows
    autoplay
    height="400px"
  >
    <q-carousel-slide img-src="statics/images/papercut1.jpg"/>
    <q-carousel-slide img-src="statics/images/papercut2.jpg"/>
  </q-carousel>
</template>
```

### 加入文字区块 ###

Quasar在`carousel`中有个子组件`QCarouselControl`用来自定义按钮在页面上。

根据官方文档的范例，`QCarouselControl`要放在`QCarousel`的最后面，也就是`QCarouselSlide`的后面。

```html
<q-carousel-control
  position="center"
  slot="control-nav"
  slot-scope="carousel"
  class="carouselInput">
</q-carousel-control>
```

在`q-carousel-control`中加入内容：

```html
<div class="main">
  <h6 class="title">新锐旅游网站</h6>
  <p class="subtitle">您身边的好玩专家</p>
  <p>发现周边好玩的地方，玩得快乐，玩得精彩。</p>
</div>
```

### 加上CSS ###

```css
<style lang="stylus" scoped>
  .carouselInput {
    width: 90%
  }

  .carouselInput .main {
    text-align center
    color: #f50057
  }

  .carouselInput .title {
    font-size 48px
  }

  .carouselInput .subtitle {
    font-size 24px
  }
</style>
```

### 调整手机版CSS ###

```css
@media (min-width: 768px) {
  .carouselInput .title {
    font-size 48px
  }

  .carouselInput .subtitle {
    font-size 24px
  }
}

@media (max-width: 768px) {
  .carouselInput .title {
    font-size 24px
  }

  .carouselInput .subtitle {
    font-size 16px
  }
}
```

## 旅游网站-搜索框 ##

### 加入搜索框 ###

**`input`**

首先到`quasar.config.js`中引入`QInput`

```javascript
framework: {
  components: ['QInput']
}
```

在`<div class="main">`后面加入`q-input`内容：

```html
<q-input
  inverted-light
  color="white"
  placeholder="输入城市/景点 或是想去的地方"
  :after="[{icon:'fas fa-search-location'}]"
  v-model="search">
</q-input>
```

- `inverted`显示**背景**
- `color`主题颜色
- `after`用来显示输入框前后`icon`

最后绑定`v-model="search"`，此时需要在`data`中添加`value`值，否则会报错。

```javascript
  data() {
    return {
      search: ''
    }
  }
```

### 调整排版 ###

> 使用[Flex CSS](http://www.quasarchs.com/components/flex-css.html)调整组件长度。

```html
<div class="row">
  <div class="col-md-2 col-xs-1"></div>
  <div class="col-md-8 col-xs-10">
    <q-input ...></q-input>
  </div>
  <div class="col-md-2 col-xs-1"></div>
</div>
```

### 自动填入`autocomplete` ###

引入`QAutocomplete`组件：

```javascript
framework: {
  components: ['QAutocomplete']
}
```

加入`q-autocomplete`：

```html
<q-input ...>
  <q-autocomplete :static-data="{field: 'label', list: countries}"/>
</q-input>
```

- `static-data`
    - `field`用于搜索数据的栏位
    - `list`搜索的数据来源

### 设置静态数据 ###

```javascript
countries: [
  {label: '广州市', icon: 'fas fa-map-marker-alt'},
  {label: '深圳市', icon: 'fas fa-map-marker-alt'},
  {label: '珠海市', icon: 'fas fa-map-marker-alt'},
  {label: '[网美景点]香山公园，秋季赏枫胜地', stamp: '北京市'},
  {label: '珠海长隆[海豚剧场]精彩不容错过！精彩变身演出抢先看', 
   stamp: '珠海，长隆', rightTextColor: 'pink-13'}
]
```

### 自定义过滤器filter ###

在`q-autocomplete`中加入`filter`：

```html
<q-autocomplete
  :static-data="{field: 'label', list: countries}"
  :filter="advFilter"
/>
```

引入`lodash`处理`filter`。

## 旅游网站-Popover弹出框 ##

### 加入Popover组件 ###

在`quasar.config.js`中引入`QPopover`。[Popover](http://www.quasarchs.com/components/popover.html)

- `no-focus`不设焦点
- `fit`弹出框跟输入框等长
- `v-show="!search"`弹框和候选框不同时出现

### 内容排版 ###

使用`FlexCSS`来进行排版。

```html
<div class="row viewList">
  <div class="col-sm-4 col-xs-12"></div>
  <div class="col-sm-4 col-xs-12"></div>
  <div class="col-sm-4 col-xs-12"></div>
</div>
```

设配手机端，在CSS底部加入：

```css
@media (max-width: 576px) {
  .viewList {
    width: 280px
  }
}
```

解决在手机像素下原来`Popover`不能自动`fix`的问。这里应该是小于Popover的`fix`的**最小宽度**。

### 设置内容(List&Item) ###

列表类直接用`list`做最快。

```html
<div class="col-sm-4 col-xs-12">
  <q-list>
    <q-list-header>热门目的地</q-list-header>
    <q-item>
      <q-item-main>珠海</q-item-main>
    </q-item>
  </q-list>
</div>
```

### 加入右侧Icon及文字 ###

在`src/components`下新建`LIcon.vue`，提升组件复用。

主要使用了`q-icon`来引入[Font Awesome](http://www.fontawesome.com.cn/)的`icon`。

### 在原来的页面引入子组件 ###

> 具体代码：
> [SectionCarousel.vue](https://github.com/whjin/make-quasar/blob/master/src/pages/Index/SectionCarousel.vue)
> [src/components/LIcon.vue](https://github.com/whjin/make-quasar/blob/master/src/components/LIcon.vue)

## 旅游网站-Cards卡片 ##

### 建立并引入第二个区块 ###

在`src/pages/Index`下新建`SectionCards.vue`组件，用来作为卡片区块。

在`Index.vue`中引入`SectionCards.vue`。

### 区块内版面规划 ###

```html
<div class="row">
  <div class="col-12"><b>本月最精选</b></div>
  <div class="col-lg-3 col-sm-6 col-xs-12">卡片一</div>
  <div class="col-lg-3 col-sm-6 col-xs-12">卡片二</div>
  <div class="col-lg-3 col-sm-6 col-xs-12">卡片三</div>
  <div class="col-lg-3 col-sm-6 col-xs-12">卡片四</div>
</div>
```

### 制作卡片 ###

卡片内的内容都会大量重复，所以直接把卡片独立成一个组件。

在`src/components/`下新建一个`LCard.vue`。

> 在`quasar.config.js`中引入卡片组件[Cards](http://www.quasarchs.com/components/card.html)

```javascript
framework: {
  components: [
    'QCard',
    'QCardTitle',
    'QCardMain',
    'QCardMedia',
    'QCardSeparator',
    'QCardActions'
  ]
}
```

卡片主要分成三个部分：

- `q-card-media`放照片影片的区块
- `q-card-title`卡片的标题
- `q-card-main`卡片的主内容
- `q-card-actions`用来放按钮等操作的区块
- `q-card-separator`分隔线

在`SectionCards.vue`中引入`LCard.vue`。

```html
<div class="col-lg-3 col-sm-6 col-xs-12">
  <l-card/>
</div>
```

```javascript
import LCard from 'src/components/LCard.vue'
export default {
  components:{
    LCard
  },
}
```

### 加上Icon ###

继续补上**评分**和**地标**的`Icon`。

### 让LCard的文字能从父组件引入 ###

让`LCard.vue`能够动态获取数据：

<p class="codepen" data-height="365" data-theme-id="0" data-default-tab="html" data-user="whjin" data-slug-hash="OqJpKq" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="Quasar-LCard.vue">
  <span>See the Pen <a href="https://codepen.io/whjin/pen/OqJpKq/">
  Quasar-LCard.vue</a> by whjin (<a href="https://codepen.io/whjin">@whjin</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

### 在SectionCards设置数据 ###

新增一个`data`数据`monthBestList`，然后在`template`模板中使用`v-for`获取数据并显示。

```html
<template v-for="(data,index) in monthBestList">
  <div class="col-lg-3 col-sm-6 col-xs-12 q-pa-sm" :key="index">
    <l-card
      :title="data.title"
      :rate="data.rate"
      :comment="data.comment"
      :view="data.view"
      :locate="data.locate"
      :image="data.image"
    />
  </div>
</template>
```

### 调整CSS及layout ###

## 旅游网站-制作景点详情页 ##

在`src/pages`下新建`place`文件夹，并在此文件夹下新建`Index.vue`作为文章的主要页面。

### 设置Vue Router ###

要进行页面导航/切换需要用到Vue Router。

在`router/routes.js`中加入导航：

```javascript
const routes = [
  {
    path: '/',
    component: () => import('layouts/MyLayout.vue'),
    children: [
      {path: '', component: () => import('pages/Index')},
      {path: 'Place', component: () => import('pages/Place')}
    ]
  }
];
```

在`http://localhost:8080/#/place`中查看效果。

### 加入视差(Parallax)组件 ###

> [视差(Parallax)](http://www.quasarchs.com/components/parallax.html)

在`quasar.config.js`中引入`QParallax`组件。

```html
<template>
  <q-page>
    <q-parallax :src="localData.image" :height="400">
      <p>{{ localData.title }}</p>
    </q-parallax>
  </q-page>
</template>
```

### 主题部分的页面排版 ###

按照8格+4格进行排版：

```html
<div class="row place-main">
  <div class="col-8"></div>
  <div class="col-4"></div>
</div>
```

CSS补上左右`margin 5%`让页面看起来不会太满。

```css
.place-main {
  margin-left 5%
  margin-right 5%
}
```

### 设置左边画面 ###

这里要用Quasar的面包屑[BreadCrumbs](http://www.quasarchs.com/components/breadcrumbs.html)组件。

在`quasar.config.js`中引入：

```javascript
'QBreadcrumbs',
'QBreadcrumbsEl',
```

### 加上景点信息及评分的排版 ###

这里按照`8格+4格`设定，左侧栏要设为文字靠右对齐。

### 加上景点信息 ###

引入`LIcon.vue`图标组件：

```html
<div class="col-8 info-left">
  <l-icon 
    class="q-mt-sm" 
    :text="'景点编号：' + localData.id" 
    :icon="'fas fa-tag'" 
    :color="'grey'"/><br>
  ...
</div>
```

### 加上评分 ###

评分组件[Rating](http://www.quasarchs.com/components/rating.html)


## 表单组件-Field ##

> [表单字段(Field)](http://www.quasarchs.com/components/field.html)

Field的组件有`QInput`、`QSeclet`、`QDatetime`、`QChipsInput`

### 引入组件 ###

在`quasar.config.js`中引入组件

### 基本范例 ###

```html
<q-field
  label="信箱">
  <q-input suffix="@gmail.com" v-model="model"/>
</q-field>
```

- `label`设置标题文字
- `icon`设置标题的`icon`
- `icon-color`设置标题`icon`的颜色
- `helper`组件地下的辅助文字
- `error`控制组件在错误时会变成红色警示
- `error-label`错误时会显示的文字
- `warning`控制组件是否为警告状态
- `warning-label`同`error-label`
- `count`显示目前输入多少文字
- `inset`用来为没有`icon/label`的栏位留空
- `orientation`组件的排列方向（水平`horizontal`/垂直`vertical`）
- `label-width`文字区块的宽度（以`12`格宽度划分）假设文字的宽度要和输入一样长，则设定为`6`
- `dark`是文字反白，适用在暗色背景下

## 表单组件-Chips Input ##

> [Chips Input](http://www.quasarchs.com/components/chips-input.html)

```html
<q-chips-input float-label="兴趣" v-model="model" />
```

```javacript
export default {
  data() {
    return {
      model: []
    }
  }
}
```

### 外观属性 ###

- `chips-color`改变`chips`的颜色
- `chips-bg-color`改变`chips`的背景颜色
- `add-icon`替换输入时显示在右边的`enter`按钮`icon`

### 基本属性 ###

- `prefix`加入前缀文字（不影响`array`内的值）
- `suffix`加入后缀文字，可以跟前缀一起用
- `hide-underline`移除原本输入框的底线
- `no-parent-field`如果外面套有QField，可以避免跟QField的效果连结
- `upper-case`自动转大写
- `lower-case`自动转小写

**大部分组件都会重复的基本属性**

- `float-label`悬浮标题
- `stack-label`固定式标题
- `color`组件颜色
- `inverted`是否有背景色
- `inverted-light`改善亮色背景下组件的显示
- `dark`改善暗色背景下组件的显示
- `error`错误
- `warning`警告
- `disable`跟`readonly`类似，但是会有灰键效果

### 事件属性 ###

- `@input(newVal)`输入文字的同事就会触发
- `@change(newVal)`数组数值改变触发
- `@clear(clearVal)`数组被清空时触发
- `@duplicate(val)`输入重复的值时触发
- `@add(val)`输入时触发
- `@remove({index, value})`其中一个组件被删除时触发

### 方法属性(Vue Methods) ###

这里的用法通常都是在组件中加入`red`属性，然后再其他地方使用`this.$refs`来对这些组件进行操作。

- `add(value)`加入值到组件的数组中
- `remove(index)`删除指定索引的值
- `focus()`聚焦在组件上
- `select()`选择组件
- `clear()`清除组件中数组的值

## 表单组件-Radio ##

> 引入组件`QRadio`，[单选框(Radio)](http://www.quasarchs.com/components/radio.html)

### 与QField一起使用 ###

```html
<q-field
        label="黄金周去哪玩？"
        orientation="vertical">
    <q-radio v-model="model" label="去杭州" val="hangzhou"/>
    <q-radio v-model="model" label="去北京" val="beijing"/>
    <q-radio v-model="model" label="去成都" val="chengdu"/>
</q-field>
```

### 基本属性 ###

- `val`存储绑定变量的值
- `label`组件上的文字
- `left-label`设定为`true`时，文字会改变显示在选项的左边
- `checked-icon`改变选取时的icon
- `unchecked-icon`改变未选取时的icon
- `color`改变组件的颜色
- `keep-color`没选取时也会有颜色（默认是灰色）
- `readonly`只读属性
- `disable`禁用
- `dark`在暗色背景时，凸显组件文字
- `no-focus`不会触发聚焦事件

### 基本事件 ###

- `@input`选取时触发
- `@blur`失去焦点（点到其他地方）时触发
- `@focus`聚焦（点选该组件）时触发

## 表单组件-Checkbox ##

> [复选框(Checkbox)](http://www.quasarchs.com/components/checkbox.html)

### 引入组件 ###

在`quasai.config.js`中引入`QCheckbox`。

复选框需要绑定数据类型为`Array`，也需要和`QField`一起使用。

### 基本属性 ###

- `val`数值，加入到`v-model`绑定的变量中
- `true-value`如果`model`不是数组，在选取时会给`model`值`true`，用来取代`true`
- `false-value`同上解析
- `indeterminate-value`用来替换`null`
- `toggle-indeterminate`使点击可以让状态在以上三个中转换

## 表单组件-Toggle ##

> [切换键Toggle](http://www.quasarchs.com/components/toggle.html)

### 引入组件 ###

在`quasar.config.js`中引入`QToggle`

### 基本属性 ###

- `val`，`v-model`是`Array`，会加在`Array`内
- `icon`如果底下两个（`checke-icon`、`unchecked-icon`）icon 会被覆盖掉

## 表单组件-Option Group ##

> [选项组option-group](http://www.quasarchs.com/components/option-group.html)

把选项写进一个`Array`中，然后直接用`v-for`全部渲染出来。

### 引入组件 ###

每一步都是一样的，在`quasar.config.js`中引入`QOptionGroup`。

### 基本范例 ###

**CheckBox**

```html
<template>
    <q-field orientation="vertical" label="要选购的商品">
        <q-option-group
                type="checkbox"
                v-model="model"
                :options="optionList"
        />
    </q-field
    >
</template>

<script>
    export default {
        name: "index",
        data() {
            return {
                model: [],
                optionList: [
                    {label: '鸡蛋', value: 'egg'},
                    {label: '海带', value: 'seaweed'},
                    {label: '鸡腿', value: 'lag'},
                    {label: '牛肉', value: 'beef'}
                ]
            }
        }
    }
</script>
```

**`toggle`、`radio`和`checkbox`类似，只需要修改`type`属性值即可**

## 表单组件-Datetime ##

时间日期输入框Datetime，有Material和IOS两种风格。

### 引入组件 ###

有两个组件需要引入，一个是输入时显示，一个是默认就是显示的。分别为：

日期时间输入[Datetime Input](http://www.quasarchs.com/components/datetime-input.html)

```javascript
framework: {
  components: ['QDatetime']
}
```

日期时间选择器[Datetime Picker](http://www.quasarchs.com/components/datetime-picker.html)

```javascript
framework: {
  components: ['QDatetimePicker']
}
```

### 基本操作 ###

```html
// Datetime Input
<q-datetime v-model="model" type="date"/>

// Datetime Picker
<q-datetime-picker v-model="model" type="date"/>
```

### 基本属性 ###

- `type`，一共有三个值，默认是`date`
    1. `date`单纯日期
    2. `time`单纯时间
    3. `datetime`时间+日期

- `minimal`，不显示标题

- `min max`，设置能够选择的日期时间范围
```html
<q-datetime v-model="model" type="datetime" max="2019/02/27 2:30"/>
```

- `format-model`存储的时间格式，有四种选择：
    1. `auto`2019-02-27T12:01:00.000+08:00
    2. `date`"2019-02-27T04:00:00.000Z"
    3. `number`1541044860000
    4. `string`2019-02-27T12:01:00.000+08:00

- `format24h`设为24时制的时钟

### 基本方法 ###

**Input**

- `show()`显示输入
- `hide()`隐藏输入
- `toggle()`切换输入
- `clear()`清空model

**Picker**

- `setYear(val)`设置年
- `setMonth(val)`设置月
- `setDay(val)`设置日
- `setHour(val)`设置时
- `setMinute(val)`设置分
- `setView(val)`设置要显示的模式
- `clear()`清空model

## 表单组件-Editor ##

### 内建的文章编辑器Editor ###

> [编辑器（WYSIWYG）](http://www.quasarchs.com/components/editor---wysiwyg.html)

在`quasar.config.js`中引入`QEditor`组件。

```html
<q-editor v-model="model"/>
```

主要设置页面的属性有三个：

- `Toolbar`
```html
<q-editor
  v-model="model"
  :toolbar="[
      ['bold','italic','strike','underline'],
      ['hr','link'],
      ['fullscreen'],
      ['print']
    ]"
/>
```

- `Definitions`
    - `label`要显示的文字
    - `icon`要显示的icon
    - `tip`小提示
    - `cmd`如果不想用默认的功能名称，可以用这个绑回你要的功能
    - `handler`自定义`methods`的`function`名称
    ```javascript
    save: {
      label:'保存',
      handler: functionName
    }
    ```
    - `disable`禁用

```html
<q-editor
        v-model="model"
        :toolbar="[
        ['bold','italic','strike','underline'],
        ['hr','link'],
        ['fullscreen'],
        ['print']
    ]"
        :definitions="{
            bold:{label:'粗体',icon:null,tip:'这是粗体'}
            }"
/>
```

- `Font`

```html
<q-editor v-model="model"
          :toolbar="[
        ['arial','arial_black','comic_sans'],
    ]"
          :fonts="{
              arial:'Arial',
              arial_black:'Arial Black',
              comic_sans:'Comic Sans MS'
              }"
/>
```

### 基本事件 ###

- `@input`输入时触发
- `@fullscreen(true/false)`切换全屏时触发

## 表单组件-Knob旋转按钮 ##

> [旋转按钮（Knob)](http://www.quasarchs.com/components/knob.html)

在`quasar.config.js`中引入`QKnob`组件。

```html
<q-knob
        v-model="model"
        :min="0"
        :max="25"
>
    <q-icon class="q-mr-xs" name="volume_up"/>
    {{model}}
</q-knob>
```

**属性**

- `size`调整组件的大小，默认`120px`
- `step`数值的间距
- `decimals`小数点显示的位数
- `min max`最小值和最大值
- `color`、`track-color`颜色、未到达的旋转轴颜色
- `line-width`线条的宽度，默认`6px`

**事件**

- `@input(val)`改变时立即触发
- `@change(val)`改变时触发
- `@drag-value(val)`拖动时就会触发

## 弹窗-Action Sheet ##

> [操作表(ActionSheet)](http://www.quasarchs.com/components/action-sheet.html)

在`quasar.config.js`中引入`ActionSheet`组件，有Material和IOS两种风格。

**`pluginS`形式**

```javascript
framework: {
  plugins: ['ActionSheet']
}
```

**`components`形式**

```javascript
framework: {
  components: ['QActionSheet']
}
```

### 作为Plugins的使用方法 ###

**Vue内**

```javascript
this.$q.actionSheet(configObj)
```

**Vue外**

```javascript
import { ActionSheet } from 'quasar';
ActionSheet.create(configObj)
```

```javascript
this.$q.actionSheet({
    title: '操作选择',
    grid: true, //使用格状排版（一排三个）
    dismissLabel: '取消', //取消按钮的文字 只有IOS主题下可用 默认是cancel
    actions: [
        {
            label: '抓虫',
            color: 'green',
            icon: 'fas fa-bug',
            handler() {
                console.log('抓虫大师')
            }
        },
        {
            label: '分享到微博',
            color: 'blue',
            icon: 'fas fa-weibo'
        },
        {
            label: '请人帮忙',
            color: 'black',
            icon: 'fas fa-alipay'
        }
    ]
}).then(action => {}).watch(() => {});
```

### 作为Component的使用方法 ###

跟上面的操作基本上一样，只是能够多监听`@show`和`@hide`时间。

**事件**

- `@ok`点选选项时触发
- `@cancel`取消时触发
- `@show`显示时触发
- `@hide`隐藏时触发
- `@escape-key`按Esc时触发

## 弹窗-Dialog ##

基本跟上面的Action Sheet一样的操作方法。

<p class="codepen" data-height="365" data-theme-id="0" data-default-tab="js" data-user="whjin" data-slug-hash="GegPVd" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="弹出窗口-Dialog">
  <span>See the Pen <a href="https://codepen.io/whjin/pen/GegPVd/">
  弹出窗口-Dialog</a> by whjin (<a href="https://codepen.io/whjin">@whjin</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

### 作为Component的使用方法 ###

在配置文件中引入`QDialog`组件。

```html
<q-dialog>
    <span slot="title">标题</span>
    <span slot="message">正文</span>
    <span slot="body">主体</span>
    <span slot="buttons">按钮</span>
</q-dialog>
```

## 弹窗-Modal ##

> [模态框(Modal)](http://www.quasarchs.com/components/modal.html)

引入`QModal`组件，另外加入`directives`的`CloseOverlay`。

使用按钮或是`method`将`modal`设为`true`才能打开`modal`。

**全页显示**

```html
<q-btn @click="model=true">Open</q-btn>
<q-modal v-model="model" content-css="padding: 50px" maximized>
    <h4>想去哪里玩？</h4>
    <p>自由行·出国度假</p>
    <p>泰国、首尔、珠海、九寨沟</p>
    <q-btn
            class="q-mt-lg"
            color="primary"
            @click="model=false"
            label="订购行程"
    />
</q-modal>
```

**最小窗口**`minimized`

设置`position`后会自动清除`content-css`定义的`css`，所以要在里面多一个`div`来做`padding`。

```html
<q-modal v-model="model" minimized>
    <div style="padding: 20px">
        ...
    </div>
</q-modal>
```

### 基本属性 ###

- `minimized`，`maximized`设置窗口最小化或是最大化
- `no-route-dismiss`、`no-esc-dismiss`、`no-backdrop-dismiss`分别为控制换页、按下Esc、按黑色背景是否会触发开闭事件
- `content-css`，`content-classes`，Modal内的CSS及class，在设置了`position`后会无效
- `position`设置弹窗出来的位置
- `position-classes`设置`position`后就要用这个来设`class`，默认是`items-center`，`justify-center`
- `transition`，`enter-class`，`leave-class`可以用自定义的CSS来做出场的动画
- `no-refocus`是否让关闭窗口时聚焦回到打开窗口前的最后一个组件

### Vue方法 ###

控制打开关闭窗口的一些方法，要搭配`this.$refs.窗口名称`来使用。

- `show`
- `hide`
- `toggle`

## 弹窗-Notify ##

> [通知框（Notify）](http://www.quasarchs.com/components/notify.html)

<p class="codepen" data-height="365" data-theme-id="0" data-default-tab="js" data-user="whjin" data-slug-hash="wOaGJO" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="弹窗-Notify">
  <span>See the Pen <a href="https://codepen.io/whjin/pen/wOaGJO/">
  弹窗-Notify</a> by whjin (<a href="https://codepen.io/whjin">@whjin</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

### 在Vue外使用 ###

```javascript
import {Notify} from 'quasar';

Notify.create('已保存');
//方式二
Notify.create({
    message: '已保存'
});
```

## 进度条-Ajax Bar&Loading Bar  ##

> [Ajax栏(Ajax Bar)](http://www.quasarchs.com/components/ajax-bar.html)

在`quasar.config.js`中引入`QAjaxBar`组件。

### 基本使用 ###

### Ajax Bar ###

因为在每个页面都会用到，所以放在最上层`App.vue`。

```html
<div id="q-app">
    <router-view></router-view>
    <a-ajax-bar/>
</div>
```

- `position`设置组件位置
- `size`载入条的宽度，默认`4px`
- `color`默认`red`
- `reverse`使进度方向相反

#### 基本事件 ####

- `@start`开始动作时触发
- `@stop`结束动作时触发

#### 基本方法 ####

- `start()`
- `stop()`

### Loading Bar ###

## 进度条-Inner Loading ##

> [内部加载(Inner Loading)](http://www.quasarchs.com/components/inner-loading.html)

### 注意事项 ###

使用InnerLoading时会作用在`relative-position`这个`class`下，如果没有添加这个会变成整页。

### 基本操作 ###

**index.vue**

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="html" data-user="whjin" data-slug-hash="rRVJYL" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="Quasar-InnerLoading-Index.vue">
  <span>See the Pen <a href="https://codepen.io/whjin/pen/rRVJYL/">
  Quasar-InnerLoading-Index.vue</a> by whjin (<a href="https://codepen.io/whjin">@whjin</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

**MyField.vue**

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="html" data-user="whjin" data-slug-hash="XGbZEN" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="Quasar-InnerLoading-MyField.vue">
  <span>See the Pen <a href="https://codepen.io/whjin/pen/XGbZEN/">
  Quasar-InnerLoading-MyField.vue</a> by whjin (<a href="https://codepen.io/whjin">@whjin</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

**效果**

![](https://i.imgur.com/d5QwW8f.jpg)

![](https://i.imgur.com/0nMNKFM.jpg)

## CSS Helpers ##

### 空间排版CSS Spacing Classes ###

> [CSS间距类CSS Spacing Classes](http://www.quasarchs.com/components/spacing.html)

### 基本范例 ###

```css
q-ma-xs
```

- `q`作为前缀
- `ma`：
    - `m`类型，`margin`
    - `a`方向，`all`
- `xs`范围的大小跟`flex css`一致

### 语法 ###

```
q-[类型][方向]-[大小]
```

- 类型
    - `m`（`margin`向外扩）
    - `p`（`padding`向内扩）

- 方法
    
总共有7种选择，除了基本的`t(top)`，`r(right)`，`l(left)`、`b(bottom)`，`a(all)`之外，还有两种`x(left+right)`，`y(top+bottom)`。

- 大小

有`none`，`auto`(只能用在`margin`),`xs`，`sm`，`md`，`lg`，`xl`。

### 阴影CSS Shadows ###

> [CSS阴影（立面图）CSS Shadows](http://www.quasarchs.com/components/shadows.html)

### 可视范围CSS Visibility ###

> [可视范围CSS Visibility](http://www.quasarchs.com/components/visibility.html)

### 位置排版CSS Positioning Classes ###

> [CSS定位类CSS Positioning Classes](http://www.quasarchs.com/components/positioning.html)

## 自定义颜色 ##

> [调色板(Color Palette)](http://www.quasarchs.com/components/color-palette.html)

在`src/css/app.styl`文件中自定义全局CSS

### 新增颜色 ###

```css
.text-redsp
  color: #D03F38
.bg-redsp
  background: #D03F38  
```

这里`text`和`bg`需要同时设定。

### 使用 ###

```html
<q-btn color="redsp">Open</q-btn>
```

## 多国语系I18n ##

### Quasar的I18n ###

> [多国语系(I18n)](http://www.quasarchs.com/components/internationalization.html)

在`quasar.config.js`中设置：

```javascript
framework: {
  i18n: 'zh-hans'
}
```

### 读取当前语系 ###

```javascript
let lang = this.#q.i18n.getLocal()
```

### 动态设置 ###

Quasar的切换语系不像是传统的`vue-i18n`直接换就能用，必须重新载入新语系的语系档。

```html
<template>
  <q-btn @click="setLang('zh-hans')">简体中文</q-btn>
</template>

<script>
  export default {
    name: "I18n",
    methods: {
      setLang(lang) {
        import('quasar-framework/i18n/${lang}').then(lang => {
          this.$q.i18n.set(lang.default)
        })
      }
    }
  }
</script>
```

### Vue-I18n ###

Vue-I18n在`src/i18n`里面，参照已经设定的内容添加自己想要的语系。

### 应用 ###

```html
<p>{{$t('apple')}}</p>
```

```html
<q-btn @click="setLang()" :label="$t('setting')"></q-btn>
```

### 动态切换语系 ###

```javascript
methods: {
    setLang() {
        this.$i18m.local = 'zh-CN'
    }
}
```

> GITHUB：[使用Quasar设计旅游网站](https://github.com/whjin/make-quasar)
> 文章链接：[使用Quasar设计Material和IOS风格的响应式网站](https://whjin.github.io/blog/2019/02/23/%E4%BD%BF%E7%94%A8Quasar%E8%AE%BE%E8%AE%A1Material%E5%92%8CIOS%E9%A3%8E%E6%A0%BC%E7%9A%84%E5%93%8D%E5%BA%94%E5%BC%8F%E7%BD%91%E7%AB%99/)