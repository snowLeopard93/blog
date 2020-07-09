## ES6入门笔记（二）

?> 本部分主要介绍四点内容，第一点是**函数**和**Symbol**，第二点是**Set**和**Map**，第三点是**Set、Map和数组的比较**，第四点是**类型转换**。

### 一、函数、Symbol

#### 1、函数

> **函数参数的默认值** 

（1）参数变量是默认声明的，所以不能用`let`或`const`再次声明。

（2）利用参数默认值，可以指定某一个参数不得省略，如果省略就抛出一个错误。

**示例：**
```javascript
function log(x, y = 'World') {
  console.log(x, y);
}

log('Hello'); // Hello World
log('Hello', 'China'); // Hello China
log('Hello', ''); // Hello
```

> **rest参数**

ES6 引入 rest 参数（形式为`...变量名`），用于获取函数的多余参数，这样就不需要使用arguments对象了。rest 参数搭配的变量是一个数组，该变量将多余的参数放入数组中。

!> rest 参数之后不能再有其他参数（即只能是最后一个参数），否则会报错。

**示例：**

```javascript
function add(...values) {
  let sum = 0;
  for (var val of values) {
    sum += val;
  }
  return sum;
}
add(2, 5, 3) // 10
```

> **箭头函数**

ES6 允许使用“箭头”（`=>`）定义函数。

!> 箭头函数有几个使用注意点：

?> （1）函数体内的this对象，就是**定义时所在的对象**，而不是使用时所在的对象。
（2）不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。
（3）不可以使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用`rest`参数代替。
（4）不可以使用`yield`命令，因此箭头函数不能用作`Generator`函数。

**示例1：**

```javascript
var f = () => 5;
// 等同于
var f = function () { return 5 };

var sum = (num1, num2) => num1 + num2;
var sum = (num1, num2) => { return num1 + num2; };

// 等同于
var sum = function(num1, num2) {
  return num1 + num2;
};
```

**示例2：**

```javascript
function foo() {
  setTimeout(() => {
    console.log('id:', this.id);
  }, 100);
}

var id = 21;

foo.call({ id: 42 });
```

**注：**`setTimeout`的参数是一个箭头函数，这个箭头函数的定义生效是在foo函数生成时，而它的真正执行要等到 100 毫秒后。如果是普通函数，执行时this应该指向全局对象window，这时应该输出21。但是，箭头函数导致this总是指向函数定义生效时所在的对象（本例是{id: 42}），所以输出的是42。

**示例3：**

箭头函数可以让`setTimeout`里面的this，绑定定义时所在的作用域，而不是指向运行时所在的作用域。

```javascript
function Timer() {
  this.s1 = 0;
  this.s2 = 0;
  // 箭头函数
  setInterval(() => this.s1++, 1000);
  // 普通函数
  setInterval(function () {
    this.s2++;
  }, 1000);
}

var timer = new Timer();

setTimeout(() => console.log('s1: ', timer.s1), 3100);
setTimeout(() => console.log('s2: ', timer.s2), 3100);
// s1: 3
// s2: 0
```

上面代码中，Timer函数内部设置了两个定时器，分别使用了箭头函数和普通函数。前者的this绑定定义时所在的作用域（即Timer函数），后者的this指向运行时所在的作用域（即全局对象）。所以，3100 毫秒之后，timer.s1被更新了 3 次，而timer.s2一次都没更新。

!> 箭头函数可以让this指向固定化，这种特性很有利于封装回调函数。


#### 2、Symbol

> **基本语法**

?> （1）`Symbol`函数的参数只是表示对当前 `Symbol` 值的描述，因此**相同参数**的`Symbol`函数的返回值是不相等的。

**示例：**

```javascript
// 没有参数的情况
let s1 = Symbol();
let s2 = Symbol();

s1 === s2; // false

// 有参数的情况
let s1 = Symbol('foo');
let s2 = Symbol('foo');

s1 === s2 // false
```

?> （2）**应用场景**：消除魔术字符串；为对象定义一些非私有的、但又希望只用于内部的方法。

**注：**魔术字符串指的是，在代码之中多次出现、与代码形成强耦合的某一个具体的字符串或者数值。

**示例1：**

```javascript
// 原先的写法：
// const shapeType = {
//   triangle: 'Triangle'
// };

// 新的写法：
const shapeType = {
  triangle: Symbol()
};

function getArea(shape, options) {
  let area = 0;
  switch (shape) {
    case shapeType.triangle:
      area = .5 * options.width * options.height;
      break;
  }
  return area;
}

getArea(shapeType.triangle, { width: 100, height: 100 });
```

**示例2：**

```javascript
let size = Symbol('size');

class Collection {
  constructor() {
    this[size] = 0;
  }

  add(item) {
    this[this[size]] = item;
    this[size]++;
  }

  static sizeOf(instance) {
    return instance[size];
  }
}

let x = new Collection();
Collection.sizeOf(x); // 0

x.add('foo');
Collection.sizeOf(x); // 1

Object.keys(x); // ['0']
Object.getOwnPropertyNames(x); // ['0']
Object.getOwnPropertySymbols(x) // [Symbol(size)]
```

> **常用方法**

**（1）`Object.getOwnPropertySymbols()`**

?> `Object.getOwnPropertySymbols()`用来获取所有 `Symbol` 属性名。

**（2）`Symbol.for()`**

?> `Symbol.for()`接受一个字符串作为参数，然后搜索有没有以该参数作为名称的 Symbol 值。如果有，就返回这个 Symbol 值，否则就新建一个以该字符串为名称的 Symbol 值，并将其注册到全局。

**示例1：**

```javascript
let s1 = Symbol.for('foo');
let s2 = Symbol.for('foo');

s1 === s2 // true
```

**示例2：**

```javascript
Symbol.for("bar") === Symbol.for("bar");  // true

Symbol("bar") === Symbol("bar");  // false
```

**（3）`Symbol.keyfor()`**

?>`Symbol.keyFor()`返回一个已登记的 Symbol 类型值的key。

**示例1：**

```javascript
let s1 = Symbol.for("foo");
Symbol.keyFor(s1); // "foo"

let s2 = Symbol("foo");
Symbol.keyFor(s2) // undefined
```

### 二、Set、Map
#### 1、Set

> **应用场景**

?> **（1）数组去重、字符串去重**

**示例：**

```javascript
var array = [1, 2, 3, 4, 5, 5, 6];
[...new Set(array)]; // [1, 2, 3, 4, 5, 6]

[...new Set('ababbc')].join('') // “abc”
```

?> **（2）实现数组的并集、交集和差集**

**示例：**

```javascript
let a = new Set([1, 2, 3]);
let b = new Set([4, 3, 2]);

// 并集
let union = new Set([...a, ...b]);
// Set {1, 2, 3, 4}

// 交集
let intersect = new Set([...a].filter(x => b.has(x)));
// set {2, 3}

// （a 相对于 b 的）差集
let difference = new Set([...a].filter(x => !b.has(x)));
// Set {1}
```

> **常用方法**

**（1）操作方法：**

`Set.prototype.add(value)`：添加某个值，返回 Set 结构本身。

`Set.prototype.delete(value)`：删除某个值，返回一个布尔值，表示删除是否成功。

`Set.prototype.has(value)`：返回一个布尔值，表示该值是否为Set的成员。

`Set.prototype.clear()`：清除所有成员，没有返回值。

**（2）遍历方法：**

`Set.prototype.keys()`：返回键名的遍历器

`Set.prototype.values()`：返回键值的遍历器

`Set.prototype.entries()`：返回键值对的遍历器

`Set.prototype.forEach()`：使用回调函数遍历每个成员

#### 2、Map

> **基本语法**

**示例：**

```javascript
const map = new Map();

map
.set(1, 'aaa')
.set(1, 'bbb');

map.get(1) // "bbb"
```

!> （1）只有对**同一个对象的引用**，Map 结构才将其视为同一个键。（2）Map 的键实际上是跟**内存地址**绑定的，只要内存地址不一样，就视为两个键。

> **常用方法**

**（1）属性和操作方法：**

`size`

`Map.prototype.set(key, value)`

`Map.prototype.get(key)`

`Map.prototype.has(key)`

`Map.prototype.delete(key)`

`Map.prototype.clear()`

**（2）遍历方法：**

`Map.prototype.keys()`：返回键名的遍历器。

`Map.prototype.values()`：返回键值的遍历器。

`Map.prototype.entries()`：返回所有成员的遍历器。

`Map.prototype.forEach()`：遍历 Map 的所有成员。

### 三、Set、Map和数组的比较

|      | **Set**     | **Map**         | **数组**          |
| ------------- |-------------|------------- |-------------|
| **存放内容** | 值 | 键值对 |  值 |
| **是否重复** | 不重复 | 不重复 | 可以重复 |
| **添加** | set(key, value) | set(key, value)  | push()、unshift() | 
| **删除** | delete(value) | delete(key)  | splice() |
| **查询某个值** | has(value) | get(key)、has(key) | includes() |
| **清除** | clear() | clear() | |
| **获取keys** | keys() | keys() | keys() |
| **获取values** | values() | values() | values() |
| **获取entries** | entries() | entries() | entries() |
| **遍历** | forEach() | forEach() | forEach() |

### 四、类型转换

> **（1）数组转对象**

```javascript
Object.fromEntries([
  ["key1", "key2"],
  ["aa", "bb"]
]);
// { key1: "aa", key2: "bb" }
```

> **（2）数组转Map**

```javascript
new Map([
  [true, 7],
  [{foo: 3}, ['abc']]
])
// Map {
//   true => 7,
//   Object {foo: 3} => ['abc']
// }
```

> **（3）对象转数组**

```javascript
const obj = { "key1": "aa", "key2": "bb" };
Object.entries(obj);
// [ ["key1", "aa"], ["key2", "bb"] ]
```

> **（4）对象转Map**

```javascript
let obj = {"a":1, "b":2};
let map = new Map(Object.entries(obj));
```

> **（5）Map转数组**

```javascript
const myMap = new Map()
  .set(true, 7)
  .set({foo: 3}, ['abc']);
[...myMap]
// [ [ true, 7 ], [ { foo: 3 }, [ 'abc' ] ] ]
```

> **（6）Map转对象**

```javascript
function strMapToObj(strMap) {
  let obj = Object.create(null);
  for (let [k,v] of strMap) {
    obj[k] = v;
  }
  return obj;
}

const myMap = new Map()
  .set('yes', true)
  .set('no', false);
strMapToObj(myMap)
// { yes: true, no: false }
```

> **（7）Map转JSON**

```javascript
function strMapToJson(strMap) {
  return JSON.stringify(strMapToObj(strMap));
}

let myMap = new Map().set('yes', true).set('no', false);
strMapToJson(myMap);
// '{"yes":true,"no":false}'

function mapToArrayJson(map) {
  return JSON.stringify([...map]);
}

let myMap = new Map().set(true, 7).set({foo: 3}, ['abc']);
mapToArrayJson(myMap)
// '[[true,7],[{"foo":3},["abc"]]]'
```

> **（8）JSON转Map**

```javascript
function jsonToStrMap(jsonStr) {
  return objToStrMap(JSON.parse(jsonStr));
}

jsonToStrMap('{"yes": true, "no": false}');
// Map {'yes' => true, 'no' => false}

function jsonToMap(jsonStr) {
  return new Map(JSON.parse(jsonStr));
}

jsonToMap('[[true,7],[{"foo":3},["abc"]]]')
// Map {true => 7, Object {foo: 3} => ['abc']}
```

**参考：**

[ES6入门教程](https://es6.ruanyifeng.com/)
