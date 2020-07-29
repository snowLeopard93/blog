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