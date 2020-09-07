
### 一、接口

```typescript
interface Person {
    name: string;
    age: number;
}
```

#### 1、可选属性

```typescript
interface Person {
    name: string;
    age?: number;
}
```

#### 2、任意属性

```typescript
interface Person {
    name: string;
    age?: number;
    [propName: string]: any;
}
```

**注意：**

> 一旦定义了任意属性，那么确定属性和可选属性的类型都必须是它的类型的子集。

> 一个接口中只能定义一个任意属性。

#### 3、只读属性

```typescript
interface Person {
    readonly id: number;
    name: string;
    age?: number;
    [propName: string]: any;
}
```

**注意：**

> 只读的约束存在于第一次给对象赋值的时候，而不是第一次给只读属性赋值的时候。（只能在对象刚刚创建的时候修改其值）


**参考：**

[TypeScript 中文手册-接口](https://typescript.bootcss.com/interfaces.html)

[TypeScript 入门教程-接口](https://ts.xcatliu.com/basics/type-of-object-interfaces.html)