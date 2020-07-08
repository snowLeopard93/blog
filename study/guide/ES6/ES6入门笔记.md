## ES6入门笔记

本部分主要介绍**ES6常用方法**、**常用方法对照**和**方法比较**。

其中，**ES6常用方法**主要包括字符串、数值、数组和对象的常用方法；**常用方法对照**有两个维度，一个维度是**方法的类型**，包括数组、字符串、对象、数值和其他，另外一个维度是**使用的语法**，包括ES5及以前、ES6、underscore和jQuery等四种；**方法比较**则是针对第二点列出的各种方法进行比较。

### 一、ES6常用方法

**1. 字符串**

> **includes()、startsWith()、endsWith()** 

`includes()` 返回布尔值，表示是否找到了参数字符串；`startsWith()` 返回布尔值，表示参数字符串是否在原字符串的头部；`endsWith()` 返回布尔值，表示参数字符串是否在原字符串的尾部。

> **padStart()、padEnd()**

ES2017 引入了字符串补全长度的功能。如果某个字符串不够指定长度，会在头部或尾部补全。`padStart()`用于头部补全，`padEnd()`用于尾部补全。

> **trimStart()、trimEnd()**

ES2019 对字符串实例新增了`trimStart()`和`trimEnd()`这两个方法。它们的行为与`trim()`一致，`trimStart()`消除字符串头部的空格，`trimEnd()`消除尾部的空格。它们返回的都是新字符串，不会修改原始字符串。

**2. 数值**

> **Number.isFinite()、Number.isNaN()**

ES6 在Number对象上，新提供了`Number.isFinite()`和`Number.isNaN()`两个方法。

`Number.isFinite()`用来检查一个数值是否为有限的（finite），即不是Infinity。

`Number.isNaN()`用来检查一个值是否为NaN。

> **Number.parseInt()、Number.parseFloat()**

ES6 将全局方法`parseInt()`和`parseFloat()`移植到Number对象上面，行为完全保持不变。

> **Number.isInteger()**

`Number.isInteger()`用来判断一个数值是否为整数。

**3. 数组**

> **扩展运算符...**

（1）复制数组；

（2）合并数组；

（3）与解构赋值结合；

（4）字符串；

> **Array.from()**

> **Array.of()**

`Array.of()`用于将一组值，转换为数组。

> **find()、findIndex()**

`find()`用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为true的成员，然后返回该成员。如果没有符合条件的成员，则返回undefined。

`findIndex()`用于找出第一个符合条件的数组成员，然后返回第一个符合条件的数组成员的位置。如果没有符合条件的成员，则返回-1。

> **fill()**

`fill()`使用给定值，填充一个数组。

> **entries()，keys() 和 values()**

> **includes()**

`Array.prototype.includes()`返回一个布尔值，表示某个数组是否包含给定的值。

> **flat()**

`Array.prototype.flat()`用于将嵌套的数组“拉平”，变成一维的数组。该方法返回一个新数组，对原数据没有影响。

**示例：**

```javascript
[1, 2, [3, 4]].flat()
// [1, 2, 3, 4]
```

>

**4. 对象**

> **Object.is()**

**注意：** `===` 与 `Object.is()`的区别：
```javascript
+0 === -0; //true
NaN === NaN; // false

Object.is(+0, -0);// false
Object.is(NaN, NaN); // true

```

> **Object.assign()**

`Object.assign()`用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。

> **Object.values()，Object.entries()**

`Object.values()`返回一个数组，成员是参数对象自身的（不含继承的）所有**可遍历（enumerable）**属性的键值。

`Object.entries()`返回一个数组，成员是参数对象自身的（不含继承的）所有**可遍历（enumerable）**属性的键值对数组。

> **Object.fromEntries()**

`Object.fromEntries()`是`Object.entries()`的逆操作，用于将一个键值对数组转为对象。

>

### 二、常用方法对照

#### 1. 数组相关
| **作用**          | **ES5及以前** |  **ES6**         | **underscore**          | **jQuery**         |
| ------------- |-------------|------------- |-------------|-------------|
| **遍历数组** | forEach()**（ES5）** | entries()、keys()、values() | _.each() | $.each() |
| **判断数组中是否包含指定值** | indexOf() | includes() **（ES2016）** |  |
| **查询数组中指定值的第一条数据** | | find() | _.findWhere() | 
| **判断数组中是否存在符合条件的数据** | some()**（ES5）** | |  |
| **查询数组中符合条件的数据** | filter()**（ES5）** |  |  _.where()、  _.filter()  | $.grep() |
| **对数组进行排序** | sort() | sort() | _.sortBy() | |
| **查找数组中的最大值** | |  | _.max() | |
| **查找数组中的最小值** | | | _.min() | |
| **数组拷贝** | | ...**（扩展运算符）** | _.extend() | $.extend() |
| **判断是否是数组** | Array.isArray() |  | _.isArray() | $.isArray() |
| **数组做并集** | concat() | ...**（扩展运算符）** | _.union() | $.merge() |
| **数组去重** | |  | _.uniq() | |
| **获取数组中指定值的下标** | indexOf() | findIndex() | _.indexOf() | |
| **数组拉平** | | flat() | _.flatten() | |
| **数组转对象** | | Object.fromEntries() | _.object() | |

#### 2. 字符串相关
| **作用**     | **ES5及以前**     | **ES6**         | **underscore**          | **jQuery**         |
| ------------- |-------------|------------- |-------------|-------------|
| **去除字符串的前后空格** | trim()**（ES5）** | trimStart()、trimEnd() |  | $.trim() |
| **判断字符串中是否存在某个子串** | indexOf() | includes()、startsWith()、endsWith() | _.contains() | 
| **判断是否是字符串** | |  | _.isString() | 
| **补全字符串长度** | | padStart()、 padEnd() | | 

#### 3、对象相关
| **作用**     | **ES5及以前**     | **ES6**         | **underscore**          | **jQuery**         |
| ------------- |-------------|------------- |-------------|-------------|
| **获取所有key值** | Object.keys()**（ES5）** |  | _.keys() | 
| **获取所有value值** | | Object.values() | _.values() | 
| **判断对象是否为空** | | | _.isEmpty() | $.isEmptyObject() |
| **判断是否是对象** | | | _.isObject() | 
| **对象拷贝** | | Object.assign()、...**（扩展运算符）** |  _.extend() | $.extend() |
| **对象合并** | | Object.assign()、...**（扩展运算符）** | | |
| **对象转数组** | | Object.entries() | _.pairs() | |

#### 4、数值相关
| **作用**     | **ES5及以前**     | **ES6**         | **underscore**          | **jQuery**         |
| ------------- |-------------|------------- |-------------|-------------|
| **判断是否是数值** | | | _.isNumber() | $.isNumeric() |
| **字符串转整数、浮点数** | parseInt、parseFloat | Number.parseInt()、Number.parseFloat() |  | 

#### 5、其他
| **作用**     | **ES5及以前**     | **ES6**         | **underscore**          | **jQuery**         |
| ------------- |-------------|------------- |-------------|-------------|
| **判断是否是null** | | | _.isNull() | 
| **判断是否是undefined** | | | _.isUndefined() | 
| **判断是否是NaN** | | Number.isNaN() | _.isNaN() | 


### 三、方法比较

#### 1、数组相关

##### （1）判断数组中是否包含指定值；

`indexOf()`方法用于获取数组中指定值的下标，可以通过值是否等于-1判断数组中是否包含指定值；ES6中的`includes()`方法返回的是一个布尔值；（与字符串的`includes()`类似）；

**注：** `indexOf()`方法内部使用严格相等运算符（===）进行判断，这会导致对**NaN**的误判。

```javascript
[NaN].indexOf(NaN); // -1
[NaN].includes(NaN); // true
```

##### （2）判断数组中是否存在符合条件的数据、查询出数组中符合条件的数据；

ES5中的`some()`方法返回的是一个布尔值；ES5中的`filter()`方法返回的是一个数组（里面是所有满足条件的元素）；

**注：** ES5中的`some()`方法找到符合条件的数据之后就停止遍历；ES5中的`filter()`方法则会遍历所有数据；

##### （3）数组转对象

**示例：**

```javascript
// 方法一： ES6 
Object.fromEntries([
  ["key1", "key2"],
  ["aa", "bb"]
]);
// { key1: "aa", key2: "bb" }

// 方法二：underscore
_.object(["key1", "key2"], ["aa", "bb"]);
// { key1: "aa", key2: "bb" }
```

##### （4）数组合并

```javascript
const arr1 = ['a', 'b'];
const arr2 = ['c'];
const arr3 = ['d', 'e'];

// ES5 的合并数组
arr1.concat(arr2, arr3);
// [ 'a', 'b', 'c', 'd', 'e' ]

// ES6 的合并数组
[...arr1, ...arr2, ...arr3]
// [ 'a', 'b', 'c', 'd', 'e' ]
```

#### 2、对象相关

##### （1）对象拷贝

ES6中的`Object.assign()`方法是**浅拷贝**；

```javascript
// 对象拷贝
// 方法一：
let aClone = { ...a };
// 方法二：
let aClone = Object.assign({}, a);

// 对象合并
// 方法一：
let ab = { ...a, ...b };
// 方法二：
let ab = Object.assign({}, a, b);
```

`$.extend()`方法支持**浅拷贝**和**深拷贝**；

```javascript
var originObj = {"child": {"value": "1", "label": "2"}, "name": "3"};
var targetObj = {};
// 浅拷贝
targetObj = $.extend(false, targetObj, originObj);

// 修改 targetObj 中 child 中 的 value 属性
targetObj.child.value = "4";

// 输出结果：
// originObj：
// {"child": {"value": "4", "label": "2"}, "name": "3"};

// targetObj：
// {"child": {"value": "4", "label": "2"}, "name": "3"};

// 深拷贝
targetObj = $.extend(true, targetObj, originObj);

// 修改 targetObj 中 child 中 的 value 属性
targetObj.child.value = "4";

// 输出结果：
// originObj：
// {"child": {"value": "1", "label": "2"}, "name": "3"};

// targetObj：
// {"child": {"value": "4", "label": "2"}, "name": "3"};
```

`_.extend()`方法是**浅拷贝**；
```javascript
var originObj = {"child": {"value": "1", "label": "2"}, "name": "3"};
var targetObj = {};
// 浅拷贝
targetObj = $.extend(targetObj, originObj);

// 修改 targetObj 中 child 中 的 value 属性
targetObj.child.value = "4";

// 输出结果：
// originObj：
// {"child": {"value": "4", "label": "2"}, "name": "3"};

// targetObj：
// {"child": {"value": "4", "label": "2"}, "name": "3"};
```

##### （2）对象转数组

**示例：**

```javascript
// 方法一： ES6 
const obj = { "key1": "aa", "key2": "bb" };
Object.entries(obj);
// [ ["key1", "aa"], ["key2", "bb"] ]

// 方法二：underscore
_.pairs({"key1": "aa", "key2": "bb"});
// [["key1", "aa"], ["key2", "bb"]]
```

**参考：**

（1）[ES6入门教程](https://es6.ruanyifeng.com/)

（2）[underscorejs](http://underscorejs.org/)

（3）[jQuery API](https://jquery.cuishifeng.cn/)