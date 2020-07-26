## ES6进阶笔记（二）Module

### 一、Module

#### 1、概述

**（1）** ES6 模块不是对象，而是通过`export`命令显式指定输出的代码，再通过`import`命令输入。

**（2）** ES6 可以在编译时就完成模块加载，效率要比 CommonJS 模块的加载方式高。

**（3）** ES6模块的优点：

> **不再需要UMD模块格式了，将来服务器和浏览器都会支持 ES6 模块格式。**

> **将来浏览器的新 API 就能用模块格式提供，不再必须做成全局变量或者navigator对象的属性。**

> **不再需要对象作为命名空间（比如`Math`对象），未来这些功能可以通过模块提供。**

**示例：**

```javascript
// ES6模块
import { stat, exists, readFile } from 'fs';
```

#### 2、严格模式

**（1）基本概念**

`ECMAScript 5`的**严格模式**是采用具有限制性JavaScript变体的一种方式，从而使代码显示地 脱离“马虎模式/稀松模式/懒散模式“（sloppy）模式。

**（2）严格模式的限制**

> **变量必须声明后再使用**

> **函数的参数不能有同名属性，否则报错**

**示例：**

```javascript
function sum(a, a, c) { // !!! 语法错误
  "use strict";
  return a + a + c; // 代码运行到这里会出错
}
```

> **不能使用`with`语句**

**示例：**

```javascript
"use strict";
var x = 17;
with (obj) { // !!! 语法错误
  // 如果没有开启严格模式，with中的这个x会指向with上面的那个x，还是obj.x？
  // 如果不运行代码，我们无法知道，因此，这种代码让引擎无法进行优化，速度也就会变慢。
  x;
}
```

> **不能对只读属性赋值，否则报错**

**示例：**

```javascript
"use strict";
// 给只读属性赋值
var obj2 = { get x() { return 17; } };
obj2.x = 5; // 抛出TypeError错误
```

> **不能使用前缀 0 表示八进制数，否则报错**

> **不能删除不可删除的属性，否则报错**

**示例：**

```javascript
"use strict";
delete Object.prototype; // 抛出TypeError错误
```

> 不能删除变量`delete prop`，会报错，只能删除属性`delete global[prop]`

> **`eval`不会在它的外层作用域引入变量**

> **`eval`和`arguments`不能被重新赋值**

> **`arguments`不会自动反映函数参数的变化**

> **不能使用`arguments.callee`**

> **不能使用`arguments.caller`**

> **禁止`this`指向全局对象**

**注意：** ES6 模块之中，顶层的`this`指向`undefined`，即不应该在顶层代码使用`this`。

> **不能使用`fn.caller`和`fn.arguments`获取函数调用的堆栈**

> **增加了保留字（比如`protected`、`static`和`interface`）**

**（3）严格模式的使用**

> **为脚本开启严格模式**

**示例：**

```javascript
// 整个脚本都开启严格模式的语法
"use strict";
var v = "Hi!  I'm a strict mode script!";
```

> **为函数开启严格模式**

**示例：**

```javascript
function strict() {
  // 函数级别严格模式语法
  'use strict';
  function nested() { 
    return "And so am I!"; 
  }
  return "Hi!  I'm a strict mode function!  " + nested();
}

function notStrict() { 
  return "I'm not strict."; 
}
```

**（4）严格模式的优点**

> **在严格模式下通过`this`传递给一个函数的值不会被强制转换为一个对象。**

> **在严格模式中再也不能通过广泛实现的`ECMAScript`扩展“游走于”JavaScript的栈中。**

> **严格模式下的`arguments`不会再提供访问与调用这个函数相关的变量的途径。**

#### 3、export、import命令

模块功能主要由两个命令构成：`export`和`import`。`export`命令用于规定模块的对外接口，`import`命令用于输入其他模块提供的功能。

**（1）export**

> **输出变量**

**示例：**

```javascript
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958;

export { firstName, lastName, year };
```

> **输出函数**

**示例：**

```javascript
export function multiply(x, y) {
  return x * y;
};
```

**（2）import**

**示例：**

```javascript
import { firstName, lastName, year } from './profile.js';
```

### 二、比较

**注：** 笔记中的示例代码来自于[ES6入门教程](https://es6.ruanyifeng.com/)和[严格模式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode)，后面会再对笔记中的示例代码进行补充完善和调整。

**参考：**

[Module 的语法](https://es6.ruanyifeng.com/#docs/module)

[严格模式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode)
