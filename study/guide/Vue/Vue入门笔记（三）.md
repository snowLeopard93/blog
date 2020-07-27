## Vue入门笔记（三）

### 一、计算属性和侦听属性

#### 1、计算属性

如果某个值是由其他的值经过计算或其他处理得到的，可以使用`计算属性（computed）`。

**示例1：不使用计算属性**

```html
<div id="app">
    <input type="text" v-model="valueA"/>
    <label>+</label>
    <input type="text" v-model="valueB"/>
    <button @click="sum()">确定</button>
    <label>sum is：{{sumValue}}</label>
</div>
```

```javascript
  new Vue({
        el: '#app',
        data: {
            valueA: 2,
            valueB: 3,
            sumValue: 5
        },
        methods: {
            sum: function() {
                this.sumValue = Number.parseFloat(this.valueA) + Number.parseFloat(this.valueB);
            }
        }
    })
```

**完整示例戳：**[0.computeAttr-demo1.html](https://github.com/snowLeopard93/vue-demo/blob/master/vue/basic/0.computeAttr-demo1.html)

**示例2：使用计算属性**

```html
<div id="app">
    <input type="text" v-model="valueA"/>
    <label>+</label>
    <input type="text" v-model="valueB"/>
    <label>sum is：{{getSumValue}}</label>
</div>
```

```javascript
 new Vue({
        el: '#app',
        data: {
            valueA: 2,
            valueB: 3,
            sumValue: 5
        },
        computed: {
            sumValue: function() {
                return Number.parseFloat(this.valueA) + Number.parseFloat(this.valueB);
            }
        }
    })
```

**完整示例戳：**[0.computeAttr-demo2.html](https://github.com/snowLeopard93/vue-demo/blob/master/vue/basic/0.computeAttr-demo2.html)

#### 2、侦听属性

如果需要对某一个值的变化进行监听，则可以是用`侦听属性（watch）`。

**示例：**

```html
<div id="app">
    <input type="text" v-model="valueA"/>
    <label>+</label>
    <input type="text" v-model="valueB"/>
    <label>sum is：{{sumValue}}</label>
</div>
```

```javascript
new Vue({
        el: '#app',
        data: {
            valueA: 2,
            valueB: 3,
            sumValue: 5
        },
        watch: {
            valueA: function(val) {
                this.sumValue = Number.parseFloat(val) + Number.parseFloat(this.valueB);
            },
            valueB: function(val) {
                this.sumValue = Number.parseFloat(this.valueA) + Number.parseFloat(val);
            }
        },
    })
```

**完整示例戳：**[1.watchAttr-demo1.html](https://github.com/snowLeopard93/vue-demo/blob/master/vue/basic/1.watchAttr-demo1.html)

#### 3、自定义侦听器

**待补充~~**