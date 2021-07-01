
### 一、引入X6

#### 1、npm安装

```
npm install @antv/x6 --save
```

#### 2、script标签引入
```
<script src="https://unpkg.com/@antv/x6/dist/x6.js"></script>
```

### 二、初始化设置

```javascript
let graph = new X6.Graph({
    container: document.getElementById(domId),
    // width: 6896,
    // height: 2900,
    // 网格线
    grid: true,
    // 对齐线
    snapline: {
        enabled: true
    },
    selecting: {
        enabled: true,
        rubberband: true, // 启用框选
    },
    keyboard: {
        enabled: true,
    },
    // 背景图片
    // background: {
    //     image: "",
    //     position: "center",
    //     size: {
    //         width: 6896,
    //         height: 2900
    //     },
    //     repeat: "no repeat",
    //     opacity: 1
    // }
});
```

### 三、节点

#### 1、添加节点

```javascript
graph.addNode({
    id: "1",
    label: "节点",
    x: 100,
    y: 100,
    width: 50,
    height: 50,
})
```

#### 2、修改节点

**（1）修改宽高**

**（2）修改label**

#### 3、删除节点

```javascript
graph.removeNode(node);
```

#### 4、连接桩

### 四、边

**注意：** 边需要依赖于节点存在。

#### 1、添加边

```javascript
const { Shape } = X6;
let edge = new Shape.Edge({
    source: sourceNodeId, // String，必须，起始节点 id
    target: targetNodeId, // String，必须，目标节点 id
    markup: [
        {
            tagName: 'path',
            selector: 'stroke',
        }
    ],
    attrs: {
        stroke: {
            fill: 'none',
            stroke: '#99cce7',
            connection: true,
            strokeWidth: 1,
        },
    },
});
graph.addEdge(edge);
```

#### 2、修改边

#### 3、删除边

### 五、元素

#### 1、删除元素

```javascript
graph.removeCell(cell);
```

#### 4、常用方法

**（1）判断是否是节点**

```javascript
cell.isNode()
```

**（2）判断是否是边**

```javascript
cell.isEdge()
```

### 六、事件

#### 1、节点单击

```javascript
graph.on('node:click', ({ e, node, view }) => {
});
```

#### 2、鼠标移入

```javascript
graph.on('cell:mouseenter', ({ cell }) => {
});
```

#### 3、鼠标移出

```javascript
graph.on('cell:mouseleave', ({ cell }) => {
});
```

### 七、工具箱

#### 1、节点工具

```javascript
node.addTools([
    {
        name: 'boundary',
        args: {
            attrs: {
                fill: '#7c68fc',
                stroke: '#333',
                stroke-width: 1,
                fill-opacity: 0.2,
            },
        },
    },
    {
        name: 'button-remove',
        args: {
            x: 0,
            y: 0,
            offset: { x: 10, y: 10 },
        },
    },
])
```

#### 2、边工具

```javascript
edge.addTools([
    {
        name: 'boundary',
        args: {
            attrs: {
                fill: '#7c68fc',
                stroke: '#333',
                stroke-width: 1,
                fill-opacity: 0.2,
            },
        },
    },
    {
        name: 'button-remove',
        args: {
            x: 0,
            y: 0,
            offset: { x: 10, y: 10 },
        },
    },
    {
        // 路径点工具
        name: 'vertices'
    },
    {
        // 线段工具
        name: 'segments'
    }
])
```

#### 3、（元素）移除工具

```javascript
cell.removeTools();
```

**参考**

[antV-X6](https://x6.antv.vision/zh/docs/tutorial/about)

[antV-X6图表示例](https://x6.antv.vision/zh/examples)

[antV-使用工具](https://x6.antv.vision/zh/docs/tutorial/intermediate/tools)