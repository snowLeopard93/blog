## ES6入门笔记

### 一、ES6常用方法

**1. 字符串的新增方法：**

> **includes()、startsWith()、endsWith()** 

`includes()` 返回布尔值，表示是否找到了参数字符串；`startsWith()` 返回布尔值，表示参数字符串是否在原字符串的头部；`endsWith()` 返回布尔值，表示参数字符串是否在原字符串的尾部。

> **padStart()、padEnd()**

ES2017 引入了字符串补全长度的功能。如果某个字符串不够指定长度，会在头部或尾部补全。`padStart()`用于头部补全，`padEnd()`用于尾部补全。

> **trimStart()、trimEnd()**

ES2019 对字符串实例新增了`trimStart()`和`trimEnd()`这两个方法。它们的行为与`trim()`一致，`trimStart()`消除字符串头部的空格，`trimEnd()`消除尾部的空格。它们返回的都是新字符串，不会修改原始字符串。

**2. 数值的扩展：**

> **Number.isFinite()、Number.isNaN()**

ES6 在Number对象上，新提供了`Number.isFinite()`和`Number.isNaN()`两个方法。

`Number.isFinite()`用来检查一个数值是否为有限的（finite），即不是Infinity。

`Number.isNaN()`用来检查一个值是否为NaN。

> **Number.parseInt()、Number.parseFloat()**

ES6 将全局方法`parseInt()`和`parseFloat()`移植到Number对象上面，行为完全保持不变。

> **Number.isInteger()**

`Number.isInteger()`用来判断一个数值是否为整数。

### 二、常用方法对照

#### 1. 数组相关
| **作用**          | **ES5及以前** |  **ES6**         | **underscore**          | **jQuery**         |
| ------------- |-------------|------------- |-------------|-------------|
| **遍历数组** | | entries()、keys()、values() | _.each() | $.each()
| **获取数组中的所有key值** | | | _.keys() | 
| **获取数组中的所有value值** | |  | _.values() | 
| **查询数组中对应的值** | | find() | _.findWhere() | 
| **查询数组中符合条件的数据** | | includes() **（ES2016）** | _.filter() | $.grep()
| **对数组进行排序** | sort() | sort() | _.sortBy() | 
| **查找数组中的最大值** | |  | _.max() | 
| **查找数组中的最小值** | | | _.min() | 
| **拷贝数组（深拷贝、浅拷贝）** | | ...**（扩展运算符）** | _.extend() | $.extend()
| **判断是否是数组** | Array.isArray() |  | _.isArray() | $.isArray()
| **数组做并集** | concat() | ...**（扩展运算符）** | _.union() | $.merge()
| **数组去重** | |  | _.uniq() | 
| **获取数组中指定值的下标** | indexOf() | findIndex() | _.indexOf() | 

#### 2. 其他
| **作用**     | **ES5及以前**     | **ES6**         | **underscore**          | **jQuery**         |
| ------------- |-------------|------------- |-------------|-------------|
| **判断对象是否为空** | | | _.isEmpty() | $.isEmptyObject()
| **去除字符串的前后空格** | trim() | trimStart()、trimEnd() |  | $.trim()
| **判断字符串中是否存在某个子串** | indexOf() | includes()、startsWith()、endsWith() | _.contains() | 
| **判断是否是数值** | | | _.isNumber() | $.isNumeric()
| **判断是否是对象** | | | _.isObject() | 
| **判断是否是null** | | | _.isNull() | 
| **判断是否是undefined** | | | _.isUndefined() | 
| **判断是否是NaN** | | Number.isNaN() | _.isNaN() | 
| **判断是否是字符串** | |  | _.isString() | 
| **字符串转整数、浮点数** | parseInt、parseFloat | Number.parseInt()、Number.parseFloat() |  | 

**参考：**

[ES6入门教程](https://es6.ruanyifeng.com/)