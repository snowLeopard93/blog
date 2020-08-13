## Vue入门笔记（三）

### 一、组件定义、注册及使用

#### 1、组件定义

**示例：**

```javascript
Vue.component('hello-vue', {
    // 此处即为需要封装的html部分
    template: '<div>Hello World，Hello Vue！</div>'
 });
```

> **在html中定义**

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

**完整示例戳：**[0.HelloVue.html](https://github.com/snowLeopard93/vue-demo/blob/master/vue/component/0.HelloVue.html)

> **在.vue文件中定义**

```vue
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>
```

**完整示例戳：** [HelloWorld.vue](https://github.com/snowLeopard93/vue-demo/blob/master/vue-cli/src/components/HelloWorld.vue)

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

#### 4、通过 Prop 向子组件传递数据

**示例：**

```html
<div id="app">
    <blog-post v-for="item in list"
               v-bind:key="item.id"
               v-bind:title="item.title">
    </blog-post>
</div>
<script>
    Vue.component('blog-post', {
        props: ['title'],
        template: '<h3>{{ title }}</h3>'
    });
    new Vue({
        el: '#app',
        data: {
            list: [
                { id: 1, title: 'My journey with Vue' },
                { id: 2, title: 'Blogging with Vue' },
                { id: 3, title: 'Why Vue is so fun' }
            ]
        }
    })
</script>
```

**完整示例戳：**[2.prop.html](https://github.com/snowLeopard93/vue-demo/blob/master/vue/component/2.prop.html)