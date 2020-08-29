## HighCharts

### 一、前置

#### 1、HighCharts引入

> **通过script标签引入**

```html
<script src="http://cdn.highcharts.com.cn/highcharts/highcharts.js"></script>
```

> **通过require引入**

```javascript
// 先将 highcharts.js 放入到 lib 目录下，然后再通过require引入
require([
    "lib/highcharts"
], function (highcharts) {
    // ......
})
```
#### 2、HighCharts常用方法

> 初始化

```javascript
var chartOption = {
    //......
};
$("#demoDiv").highcharts(chartOption);
var demoChart = $("#demoDiv").highcharts();
```

> 自适应

```javascript
var demoChart = $('#demoDiv').highcharts();

function resizeChart(){
    demoChart && demoChart.reflow();
}

$(window).bind('resize', resizeChart);
```

### 二、常用图表简单示例

#### 1、通用属性设置

> **图例（legend）**

> **坐标轴（xAxis、yAxis）**

> **悬浮提示信息（tooltip）**

> **chart**

> **plotOptions**

#### 2. series设置

> **折线图（曲线图）**

> **柱状图（堆叠、展开）**

> **饼图（环形图）**


**参考**

[HighCharts官网](https://www.highcharts.com.cn/)

[HighCharts API](https://api.highcharts.com.cn/highcharts)

[1 分钟上手 Highcharts](https://www.highcharts.com.cn/docs/start-helloworld)