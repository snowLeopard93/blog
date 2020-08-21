## Echarts

### 一、前置

#### 1、Echarts引入

> **通过script标签引入**

```html
<script type="text/javascript" src="https://cdn.jsdelivr.net/npm/echarts/dist/echarts.min.js"></script>
```

> **通过require引入**

```javascript
// 先将 echart.min.js 放入到 lib 目录下，然后再通过require引入
require([
    "lib/echarts.min-new"
], function (echarts) {
    // ......
})
```

#### 2、Echarts初始化

```javascript
var myChart = echarts.init(document.getElementById("pieDiv"));

// option里面存放不同echarts图表的配置选项
var option = {
    // ......
};
// 将选项放入myChart对象中
myChart.setOption(option);
```

#### 3、Echarts常用方法

### 二、常用图表简单示例

### 三、Echarts复杂示例

#### 1、带图例的仪表盘

#### 2、地图

#### 3、气泡图


**参考：**

[Echarts官网](https://echarts.apache.org/)

