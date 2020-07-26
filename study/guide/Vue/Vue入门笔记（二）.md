## Vue入门笔记（二）

### 一、修饰符

#### 1、事件修饰符

> **.stop：阻止冒泡**

```html
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>
```

**完整示例戳：**[0.stop.html](https://github.com/snowLeopard93/vue-demo/blob/master/vue/modifier/0.stop.html)

> **.prevent：阻止默认事件**

```html
<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>
```

```html
<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>
```

```html
<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>
```

**完整示例戳：**[1.prevent.html](https://github.com/snowLeopard93/vue-demo/blob/master/vue/modifier/1.prevent.html)

> **.capture：添加事件监听器时使用事件捕获模式**

```html
<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即内部元素触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>
```

**完整示例戳：**[2.capture.html](https://github.com/snowLeopard93/vue-demo/blob/master/vue/modifier/2.capture.html)

> **.self：只当事件在该元素本身触发时触发回调**

```html
<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>
```

**完整示例戳：**[3.self.html](https://github.com/snowLeopard93/vue-demo/blob/master/vue/modifier/3.self.html)

> **.once：事件只触发一次**

**完整示例戳：**[4.once.html](https://github.com/snowLeopard93/vue-demo/blob/master/vue/modifier/4.once.html)

#### 2、按键修饰符

#### 3、系统修饰键

#### 4、表单修饰符

