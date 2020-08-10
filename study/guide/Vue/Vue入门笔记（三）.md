## Vue入门笔记（三）

### 一、组件基础

#### 1、定义新组件

使用`Vue.component`定义新组件

**示例：**

```javascript
Vue.component('hello-vue', {
    // 此处即为需要封装的html部分
    template: '<div>Hello World，Hello Vue！</div>'
 });
```

**完整示例戳：**[0.HelloVue.html](https://github.com/snowLeopard93/vue-demo/blob/master/vue/component/0.HelloVue.html)

#### 2、使用新组件

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

#### 3、通过 Prop 向子组件传递数据

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

### 二、组件深入

#### 1、组件注册

> **全局注册**

```javascript
Vue.component('my-component-name', {
  // ... 选项 ...
})
```

> **局部注册**

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
