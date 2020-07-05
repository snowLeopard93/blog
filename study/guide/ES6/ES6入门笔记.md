## ES6入门笔记

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

**4. 对象**

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
|**对象拷贝**| | Object.assign()、...**（扩展运算符）** |  _.extend() | $.extend() |
|**对象合并**| | Object.assign()、...**（扩展运算符）** | | |
|**对象转数组**| | Object.entries() | | |
|**数组转对象**| | Object.fromEntries() | | |

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

#### 2、对象相关

##### （1）对象拷贝和合并

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

**参考：**

（1）[ES6入门教程](https://es6.ruanyifeng.com/)

（2）[underscorejs](http://underscorejs.org/)

（3）[jQuery API](https://jquery.cuishifeng.cn/)