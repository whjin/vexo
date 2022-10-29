---
title: 状态管理与Vuex
date: 2019-08-24 09:39:56
category: ["Vue"]
tags: ["Vue.js","Vuex"]
comments: true
---

在实际的业务中，经常有跨组件共享数据的需求，`Vuex`就是设计用来统一管理组件状态的，它定义了一系列规范来使用和操作数据，使组件的应用更高效。

引入`Vuex`之后统一对共享数据进行管理存放，在各个页面中可以利用`commit`方法提交`mutation`对共享数据进行修改。

<!--more-->

```javascript
// store/index.js
export default new Vuex.Store({
  state: {
    count: 0
  },
  mutations: {
    increment: state => state.count++,
    decrement: state => state.count--
  }
})

// Component.vue
export default {
  computed: {
    count() {
      return this.$store.state.count;
    }
  },
  methods: {
    increment() {
      return this.$store.commit("increment");
    },
    decrement() {
      return this.$store.commit("decrement");
    }
  }
};
```



