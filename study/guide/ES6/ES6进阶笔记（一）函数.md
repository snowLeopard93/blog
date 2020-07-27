## ES6进阶笔记（一）函数

### 一、this

#### 1、函数内部的this指向

| **调用方式**     | **非严格模式下this指向**     | **严格模式下this指向** |
| ------------- |-------------|-------------|
| **普通函数调用** | window | undefined |
| **构造函数调用** | 实例对象 | 实例对象 |
| **对象方法调用** | 该方法所属对象 | 该方法所属对象 |
| **事件绑定方法** | 绑定事件对象 | 绑定事件对象 |
| **定时器函数** | window | window |
| **立即执行函数** | window | |

#### 2、严格模式下this指向

> **严格模式下，全局作用域函数中的this是undefined**

> **严格模式下，如果构造函数不加new调用，this会报错**
>
#### 3、改变this指向

> **apply方法**

**示例：**

```javascript
var a = {
    name: "haha"
};

function fn(v1, v2) {
    console.log(this);
    console.log(v1);
    console.log(v2);
}

fn.apply(a, ["aaa", "bbb"]);
```

> **call方法**

**示例：**

```javascript
var a = {
    name: "haha"
};

function fn(v1, v2) {
    console.log(this);
    console.log(v1 + v2);
}

fn.call(a, 1, 2);
```

> **bind方法**

**示例：**

```javascript
var a = {
    name: "haha"
};

function fn() {
    console.log(this);
}

fn.bind(a);
```

**推荐：**

[你还没搞懂this？](https://github.com/ljianshu/Blog/issues/7)

**参考：**

[2019全新javaScript进阶面向对象ES6之《函数内部的this指向》](https://www.bilibili.com/video/BV1Kt411w7MP?p=53)