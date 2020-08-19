## Vue入门笔记（三）

本部分主要介绍两点内容，第一点是**创建组件和组件注册**，第二点是**Prop基础**。 

### 一、创建组件和组件注册

#### 1、创建组件

> **使用Vue.component()创建组件**

**示例：**

```html
<script>
    Vue.component('hello-vue', {
        template: '<div>Hello World，Hello Vue！</div>'
    });
    new Vue({
        el: '#app'
    })
</script>
```

> **使用template标签创建组件**

```html
<div id="app"></div>
<template id="tmpl">
    <div>Hello World，Hello Vue！</div>
</template>
<script>
    Vue.component("hello-vue", {
        template: "#tmpl"
    });
    new Vue({
        el: '#app'
    })
</script>
```

#### 2、组件注册

> **全局注册**

```javascript
Vue.component('my-component-name', {
  // ... 选项 ...
})
```

> **局部注册**

**（1）基本语法：** 
```javascript
var ComponentA = { /* ... */ };
var ComponentB = { /* ... */ };
var ComponentC = { /* ... */ };

new Vue({
  el: '#app',
  components: {
    'component-a': ComponentA,
    'component-b': ComponentB
  }
})
```

**示例：**

```vue
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>
```

**完整示例戳：** [App.vue](https://github.com/snowLeopard93/vue-demo/blob/master/vue-cli/src/App.vue)


#### 3、组件使用

**注意：**

**（1）** `data`必须是一个函数； 

**示例：**

```html
<div id="app">
    <button-counter></button-counter>
</div>
<script>
    Vue.component('button-counter', {
        data: function () {
            return {
                count: 0
            }
        },
        template: '<button v-on:click="count++">You clicked me {{ count }} times.</button>'
    });
    new Vue({
        el: '#app'
    })
</script>
```

**完整示例戳：**[1.count.html](https://github.com/snowLeopard93/vue-demo/blob/master/vue/component/1.count.html)

### 二、Prop

#### 1、Prop类型

```javascript
props: {
  title: String,
  likes: Number,
  isPublished: Boolean,
  commentIds: Array,
  author: Object,
  callback: Function,
  contactsPromise: Promise // or any other constructor
}
```

#### 2、通过 Prop 向子组件传递数据

> **传入数字**

**示例：**

> **传入布尔值**

**示例：**

> **传入数组**

**示例：**

> **传入对象**

**示例：**

> **传入对象所有的property**

**示例：**