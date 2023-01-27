---
title: Vue组件通信
date: 2019-10-12 00:36:21
category: ["技术"]
tags: ["前端","Vue"]
---

# `props` #

父传子组件的属性，`props`值可以是一个数组或对象。

# `$emit` #

子传父组件绑定自定义事件。

<!--more-->

```javascript
// 父组件
<home @title="title">
// 子组件
this.$emit('title',[{title:'这是title'}])
```

# `vuex` #

`vuex`是一个状态管理器插件，适合数据共享多的项目。

- `state`：定义存储数据的仓库，可通过`this.$store.state`或`mapState`访问；
- `getters`：获取`store`值，可认为是`store`的计算属性，可通过`this.$store.getters`或`mapGetters`访问；
- `mutations`：同步改变`store`值，为什么会设计成同步，因为`mutation`是直接改变`store`值，`Vue`对操作进行了记录，如果是异步无法追踪改变，可通过`mapMutations`调用；
- `actions`：异步调用函数执行`mutation`，进而改变`store`值，可通过`this.$dispatch`或`mapActions`访问；
- `modules`：模块，如果状态过多，可以拆分成模块，最后在入口通过`...`解构引入。

# `parent`父实例和`children`子实例 #

- 父组件`this.$children`
- 子组件`this.$parent`

`children`和`parent`并不保证顺序，也不是响应式，只能拿到一级父组件和子组件。

# `$refs` #

```javascript
// 父组件
<home ref="home"/>

mounted(){
 // this.$refs.home 即可拿到子组件的实例,就可以直接操作 data 和 methods
}
```

# `$root` #

```javascript
// 父组件
mounted(){
  console.log(this.$root) //获取根实例，最后所有组件都是挂载到根实例上
  console.log(this.$root.$children[0]) //获取根实例的一级子组件
  console.log(this.$root.$children[0].$children[0]) //获取根实例的二级子组件
}
```

# `.sync` #

```javascript
// 父组件
<home :title.sync="title" />
//编译时会被扩展为
<home :title="title"  @update:title="val => title = val"/>

// 子组件
// 子组件可以通过$emit触发 update 方法改变
mounted(){
  this.$emit("update:title", '这是新的title')
}
```

# `v-slot` #

`v-slot`作用就是将父组件的`template`传入子组件。

插槽分类：匿名插槽（默认插槽），没有命名，有且仅有一个。

```javascript
// 父组件
<todo-list> 
    <template v-slot:default>
       任意内容
       <p>我是匿名插槽</p>
    </template>
</todo-list> 

// 子组件
<slot>我是默认值</slot>
//v-slot:default写上感觉和具名写法比较统一,容易理解,也可以不用写
```

具名插槽：相对匿名插槽组件`slot`标签带`name`命名。

```javascript
// 父组件
<todo-list> 
    <template v-slot:todo>
       任意内容
       <p>我是匿名插槽</p>
    </template>
</todo-list> 

//子组件
<slot name="todo">我是默认值</slot>
```

作用域插槽：子组件内数据可以被父页面拿到（解决了数据只能从父页面传递给子组件）

```javascript
// 父组件
<todo-list>
 <template v-slot:todo="slotProps" >
   {{slotProps.user.firstName}}
 </template> 
</todo-list> 
//slotProps 可以随意命名
//slotProps 获取的是子组件标签slot上属性数据的集合所有v-bind:user="user"

// 子组件
<slot name="todo" :user="user" :test="test">
    {{ user.lastName }}
 </slot> 
data() {
    return {
      user:{
        lastName:"Zhang",
        firstName:"san"
      },
      test:[1,2,3,4]
    }
  },
// {{ user.lastName }}是默认数据  v-slot:todo 当父页面没有(="slotProps")
```

# `EventBus` #

1. 生命一个全局Vue实例变量`EventBus`，把所有的通信数据、事件监听都存储到这个变量上；
2. 类似于Vuex，但这种方式只适用于极小的项目；
3. 原理就是利用`on`和`emit`，并实例化一个全局Vue实现数据共享；
4. 可以实现平级、嵌套组件传值，但是对应的事件名`eventTarget`必须是全局唯一的。

```javascript
// 在 main.js
Vue.prototype.$eventBus=new Vue();

// 传值组件
this.$eventBus.$emit('eventTarget','这是eventTarget传过来的值')

// 接收组件
this.$eventBus.$on("eventTarget",v=>{
  console.log('eventTarget',v);//这是eventTarget传过来的值
})
```

# 路由传参 #

1. 方案一：

```javascript
// 路由定义
{
  path: '/describe/:id',
  name: 'Describe',
  component: Describe
}
// 页面传参
this.$router.push({
  path: `/describe/${id}`,
})
// 页面获取
this.$route.params.id
```

2. 方案二：

```javascript
// 路由定义
{
  path: '/describe',
  name: 'Describe',
  omponent: Describe
}
// 页面传参
this.$router.push({
  name: 'Describe',
  params: {
    id: id
  }
})
// 页面获取
this.$route.params.id
```

3. 方案三：

```javascript
// 路由定义
{
  path: '/describe',
  name: 'Describe',
  component: Describe
}
// 页面传参
this.$router.push({
  path: '/describe',
    query: {
      id: id
  `}
)
// 页面获取
this.$route.query.id
```

三种方案对比，方案二参数不会拼接在路由后面，页面刷新参数会丢失；方案一和三参数拼接在后面，暴露了信息。

