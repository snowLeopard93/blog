## Vue进阶笔记（一）

### 一、过滤器

#### 1、全局过滤器

> **基本语法**

```javascript
Vue.filter('过滤器名称', function(data, arg, arg2){
    return data + arg + arg2;
})
```

**示例：**

```html
<div id="app">
   <div>{{msg | replaceName("不喜欢")}}</div>
</div>
<script>
    Vue.filter("replaceName", function(msg, arg){
        return msg.replace(/喜欢/g, arg);
    });
    new Vue({
        el: "#app",
        data: {
            msg: "我喜欢读书，喜欢听音乐，喜欢跑步，喜欢游泳"
        }
    })
</script>
```

**完整示例戳：**[0.globalFilter.html](https://github.com/snowLeopard93/vue-demo/blob/master/vue/advanced/0.globalFilter.html)

#### 2、私有过滤器

> **基本语法**

```javascript
new Vue({
    el: "#app",
    data: {
        msg: "111"
    },
    methods: {
        say: function() {
        
        }
    },
    filters: {
        filterName: function() {
        
        }
    }       
})
```

**示例：**

```html
<div id="app">
    <div>{{msg | replaceName("不喜欢")}}</div>
</div>
<script>
    new Vue({
        el: "#app",
        data: {
            msg: "我喜欢读书，喜欢听音乐，喜欢跑步，喜欢游泳"
        },
        filters: {
            replaceName: function(msg, arg) {
                return msg.replace(/喜欢/g, arg);
            }
        }
    })
</script>
```

**完整示例戳：**[1.privateFilter.html](https://github.com/snowLeopard93/vue-demo/blob/master/vue/advanced/1.privateFilter.html)

#### 3、注意

**（1）** 过滤器调用的时候，采取的是**就近原则**；

**（2）** 当存在同名的全局过滤器和私有过滤器时，**优先使用**私有过滤器。
