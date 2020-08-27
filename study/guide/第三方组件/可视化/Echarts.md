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
    "lib/echarts.min"
], function (echarts) {
    // ......
})
```

#### 2、Echarts常用方法

> 初始化（init）

```javascript
var demoChart = echarts.init(document.getElementById("demoDiv"));

// option里面存放不同echarts图表的配置选项
var option = {
    // ......
};
// 将选项放入 demoChart 对象中
demoChart.setOption(option);
```

> 定义主题

**（1）使用自定义的颜色**

```javascript
var theme = {
    color: [
        "#37A2DA", "#32C5E9", "#67E0E3", "#9FE6B8",
        "#FFDB5C", "#ff9f7f", "#fb7293", "#E062AE",
        "#E690D1", "#e7bcf3", "#9d96f5", "#8378EA",
        "#96BFFF"
    ]
};

var demoChart = echarts.init(document.getElementById("demoDiv"), theme);
```

**（2）引入已有的主题**

```html
<script src="echarts.js"></script>
<!-- 引入 vintage 主题 -->
<script src="theme/vintage.js"></script>
<script>
// 第二个参数可以指定前面引入的主题
var demoChart = echarts.init(document.getElementById("demoDiv"), "vintage");
demoChart.setOption({
    //...
});
</script>
```

> 绑定事件和取消绑定事件

```javascript
var demoChart = echarts.init(document.getElementById("demoDiv"));

function click() {
    //......
}
function mouseover() {
    //......
}
function mouseout() {
    //......
}

demoChart.off("mouseover");
demoChart.off("mouseout");
demoChart.off("click");
demoChart.on("mouseover", mouseover);
demoChart.on("mouseout", mouseout);
demoChart.on("click", click);
```

> 自适应（resize）

```javascript
var demoChart = echarts.init(document.getElementById("demoDiv"));

function resizeChart(){
    demoChart && demoChart.resize();
}

$(window).bind("resize", resizeChart);
```

> 销毁（dispose）

```javascript
var demoChart = echarts.init(document.getElementById("demoDiv"));
echarts.dispose(demoChart);
```

### 二、常用图表简单示例

常用图表可以根据有无坐标轴分为**有坐标轴**的图表和**无坐标轴**的图表两种。

**有坐标轴**的图表包括柱状图（条形图）、环形图（饼图）、折线图（区域图），折线图（区域图）+ 柱状图等。

**无坐标轴**的图表包括环形图（饼图）、仪表盘等。

#### 1、通用属性设置

```javascript
var options = {
    "legend": {},
    "grid": {},
    "tooltip": {},
    "xAix": [],
    "yAix": [],
    "series": []
}
```

> 图例（legend）

主要包括图例的位置，图标的字体大小等。

```javascript
"legend": {
    "show": true,
    "data": ["选项1", "选项2"],
    "textStyle": {
        "color": "#fff"
    },
    "x": "center",  //可设定图例在左、右、居中
    "y": "bottom",  //可设定图例在上、下、居中
    "orient": "vertical",
    "top": 20,
    "bottom": 20,
    "left": 10,
    "right": 10,
    "itemGap": 15
}
```

> 边距（grid）

```javascript
"grid": {
    "left": "5%",
    "right": "5%",
    "top": "5%",
    "bottom": "5%",
    "containLabel": true
}
```

> 悬浮提示信息（tooltip）

主要包括悬浮提示信息内容的格式化和字体的大小等。

```javascript
"tooltip": {
    "show": true,
    "trigger": "axis",   // 可选值： axis（有坐标轴） | item（无坐标轴）
    "formatter": "{a} <br/>{b}: {c} ({d}%)",  
    "textStyle": {
        "align": "left"
    },
    "axisPointer": {            // 坐标轴指示器，坐标轴触发有效
        "type": "shadow"        // 可选值： line（直线） | shadow（阴影）
    }
}
```

> 坐标轴（xAxis、yAix）

主要包括x轴、y轴的颜色、刻度的字体颜色，刻度的间隔等。

**（1）xAix**

```javascript
"xAxis": [
    {
        "name": "x轴",
        "type" : "category",
        "axisLabel": {
            "show": true,
            "textStyle": {
                "color": "#78cfeb"
            }
        },
        "nameTextStyle": {
            "padding": [25, 0, 0, 0]
        },
        "axisLine": {
            "lineStyle": {
                "color": "#5074a6"
            }
        },
        "data": []
    }
]
```

**（2）yAix**

```javascript
"yAxis": [
    {
        "axisLabel": {
            "show": true,
            "textStyle": {
                "color": "#5993db"
            }
        },
        "splitLine": {
            "show": true,
            "lineStyle": {
                "color": "#1f447a" // 坐标轴颜色
            }
        },
        "axisLine": {
            "lineStyle": {
                "color": "#5074a9" // 坐标轴颜色
            }
        },
        "nameTextStyle": {
            "color": "#5993db",
            "padding": [0, 60, 0, 0]
        },
        "name": "y轴",
        "min": 0,
        "max": 1000,
        "interval": 50,
        "data": []
    }
]
```


#### 2、series设置

> 有坐标轴

**（1）柱状图（条形图）（bar）**

**示例1：**

**是否堆叠（stack）**

```javascript
"series": [
    {
        name: "谷歌",
        type: "bar",
        stack: "搜索引擎",
        data: []
    },
    {
        name: "百度",
        type: "bar",
        stack: "搜索引擎",
        data: []
    }
]
```

**示例2：**

**双条形图（xAxisIndex）**

**注意：**

此时`xAxis`里面也要定义两个对象，与`series`中的对象一一对应。

series中有一个对象多了一个`xAxisIndex`属性，且值为1。

```javascript
"series": [
    {
        "name": "x轴1",
        "type": "bar",
        "label": {
            "show": true,
            "position": "right",
            "formatter": function(a) {
                                
            }
        },
        "xAxisIndex": 1,
        "data": [],
    },
    {
        "name": "x轴2",
        "type": "bar",
        "label": {
            "show": true,
            "position": "right",
            "formatter": function(a) {
                
            }
        },
        "data": []
    },
]
```

**（2）折线图（区域图）（line）**

**是否显示圆点（symbol）、曲线光滑（smooth）、阴影颜色渐变（areaStyle）**

```javascript
"series": [
    {
        "name": "系列A",
        "type": "line",
        "symbol": "none",
        "smooth": true,
        "areaStyle": {
            "normal": {
                "color": new echarts.graphic.LinearGradient(0, 0, 0, 1,[{
                        "offset": 0, color: "#0d618d" // 0% 处的颜色
                    , {
                        "offset": 1, color: "#103152" // 100% 处的颜色
                    }]
                )}
            }
        },
        "data": []
    }
]
```

**（3）折线图（区域图）+ 柱状图**

**注意：** 

此时`yAxis`里面也要定义两个对象，与`series`中的对象一一对应。

`series`中有一个对象多了一个`yAxisIndex`属性，且值为1。

```javascript
"series": [
    {
        "name": "y轴1",
        "type": "bar",
        "label": {
            "normal": {
                "show": false, //用于控制是否在图表中显示数据信息
                "position": "top",
                "distance": 15,
                "align": "center",
                "fontSize": 16,
                "rich": {
                    "name": {
                        "textBorderColor": "#fff"
                    }
                }
            }
        },
        "data": []
    },
    {
        "name": "y轴2",
        "type": "line",
        "symbol": "none",
        "smooth": true,
        // 渐变色
        "areaStyle": {
            "normal": {
                "color": new echarts.graphic.LinearGradient(0, 0, 0, 1,[{
                        offset: 0, color: "#f39700" // 0% 处的颜色
                    }, {
                        offset: 1, color: "#103152" // 100% 处的颜色
                    }]
                )
            }
        },
        "label": {
            "normal": {
                "show": false, //用于控制是否在图表中显示数据信息
                "position": "insideBottom",
                "distance": 15,
                "align": "left",
                "verticalAlign": "middle",
                "rotate": 90,
                "formatter": "{c}  {name|{a}}",
                "fontSize": 16,
                "rich": {
                    "name": {
                        "textBorderColor": "#fff"
                    }
                }
            }
        },
        "yAxisIndex": 1,
        "data": []
    }
]
```

> 无坐标轴

**（1）环形图（饼图）（pie）**

```javascript
"series": [
    {
        "name": "环形图",
        "type": "pie",
        // roseType: "radius",
        // radius: ["50%", "70%"],
        "center": ["60%", "60%"],
        "radius": "50%",
        // avoidLabelOverlap: true,
        "hoverAnimation": false,
        "itemStyle": {
            "normal": {
                // 设置阴影
                "shadowBlur": 30,
                "shadowColor": "rgba(0, 0, 0, 0.5)"
            }
        },
        "label": {
            "textStyle": {
                "color": "#fff",
                "fontSize": 16
            },
            "formatter": "{d}%"
        },
        "data": []
    }
]
```

**（2）仪表盘（gauge）**

```javascript
"series": [
    {
        "radius": 50,
        "name": "",
        "type": "gauge",
        "axisLine": { // 坐标轴线
            "lineStyle": { // 属性lineStyle控制线条样式
                "color": [[0.905,"#00fca6"],[1,"#2d4978"]],
                // shadowColor: "rgba(0, 0, 0, 0.5)",
                // shadowBlur: 10,
                "width": 15
            }
        },
        "axisLabel": {
            "show": false  // 隐藏刻度值
        },
        "axisTick": {
            "show": false  // 隐藏刻度线
        },
        "pointer": {
            "show": false // 隐藏指针
        },
        "splitLine": {
            "show": false  // 隐藏分隔线
        },
        "detail": { //最下边数值的设置
            "show": true,
            "offsetCenter": ["0", "0"],       // x, y，单位px
            "formatter": "{value}%",
            "textStyle": {       // 其余属性默认使用全局文本样式，详见TEXTSTYLE
                "fontSize": 16
            }
        },
        "data": [{"value": 90.5, name: ""}]
    }
]
```

### 三、Echarts复杂示例

#### 1、带图例的仪表盘

**实现思路：**

在options中配置`legend`、`grid`、`xAxis`、`yAxis`，在`series`中配置几个给图例用的对象，show设置为false。

```javascript
var data = [
    "avgIndex": 25.63,
    "rank": [0.5, 0.6, 0.7, 0.8]
];

var trafficCongestionChart = echarts.init(document.getElementById("trafficCongestionChart"));
var options = {
    // 其中 legend、grid、xAxis、yAxis是为显示图例而特殊设置的
    // 配置legend，这里的data，要对应type为‘bar’的series数据项的‘name’名称，作为图例的说明
    "legend": {
        "data": ["畅通", "缓行", "拥堵", "严重拥堵"],
        "selectedMode": false,  //图例禁止点击
        "itemWidth": 23,
        "itemHeight": 6,
        "textStyle": {
            "color": "black",
            "fontStyle": "normal",
            "fontWeight": "normal",
            "fontFamily": "sans-serif",
            "fontSize": 15
        },
        "x": "center",
        "y": "90%"
    },
    "grid": {
        "z": 1,//grid作为柱状图的坐标系，其层级要和仪表图层级不同，同时隐藏
        "show": false,
        "left": "-30%",
        "right": "4%",
        "bottom": "10%",
        "containLabel": true,
        "splitLine": {
            "show": false    //隐藏分割线
        }
    },
    "xAxis": [   //这里有很多的show，必须都设置成不显示
        {
            "type": "category",
            "data": [],
            "axisLine": {
                "show": false
            },
            "splitLine": {
                "show": false
            },
            "splitArea": {
                "interval": "auto",
                "show": false
            }
        }
    ],
    "yAxis": [ //这里有很多的show，必须都设置成不显示
        {
            "type" : "value",
            "axisLine": {
                "show": false
            },
            "splitLine": {
                "show": false
            }
        }
    ],
    "tooltip": {
        "formatter": function(a, b, c, d) {
            var str = "";
            if(a.value / 100 <= data.rank[1]) {
                str = "畅通";
            } else if(a.value / 100 > data.rank[1] && a.value / 100 <= data.rank[2]) {
                str = "缓行";
            } else if(a.value / 100 > data.rank[2] && a.value / 100 <= data.rank[3]) {
                str = "拥堵";
            } else if(a.value / 100 > data.rank[3]) {
                str = "严重拥堵";
            }
            return (str + "：" + a.value);
        }
    },
    "series": [
        {
            "name": "",
            "type": "gauge",
            "radius": 140,
            // startAngle: 180,
            // endAngle: 0,
            "splitNumber": 5,  //设置间隔区域的显示数量
            "detail": {
                "fontSize": 25
            },
            "axisLine": {// 坐标轴线
                "lineStyle": {// 属性lineStyle控制线条样式
                    "color": [
                        [data.rank[1], "#00ecb7"],
                        [data.rank[2], "#ffd800"],
                        [data.rank[3], "#ffae00"],
                        [1, "#ff5a00"]
                    ]
                }
            },
            "axisLabel": { //文字样式（及“10”、“20”等文字样式）
                "show": true,
                "textStyle": {
                    "color": "black",
                    "fontSize": 18
                }
            },
            "data": [{"value": data.avgIndex}]
        },
        // 以下配置是 为显示图例而做特殊设置的
        {
            "name": "畅通",
            "type": "bar",
            "data": [0],
            "barWidth": "60%",  //不显示，可以随便设置
            "itemStyle": {
                "normal": {
                    "color": "#00ecb7"  //这里的图例要注意，颜色设置和仪表盘的颜色对应起来
                }
            }
        },
        {
            "name": "缓行",
            "type": "bar",
            "data": [0],
            "barWidth": "60%",  //不显示，可以随便设置
            "itemStyle": {
                "normal": {
                    "color": "#ffd800"
                }
            }
        },
        {
            "name": "拥堵",
            "type": "bar",
            "data": [0],
            "barWidth": "60%",  //不显示，可以随便设置
            "itemStyle": {
                "normal": {
                    "color": "#ffae00"
                }
            }
        },
        {
            "name": "严重拥堵",
            "type": "bar",
            "data": [0],
            "barWidth": "60%",  //不显示，可以随便设置
            "itemStyle": {
                "normal": {
                    "color": "#ff5a00"
                }
            }
        }
    ]
};
trafficCongestionChart.setOption(options);
```

#### 2、只需用到点位的地图

如果只要用到点位，则不需要引入其他的js。

> 人口密度地图

> 点线地图

#### 3、气泡图

### 四、特殊效果实现

#### 1、每隔一段时间触发一次动画效果

> 方法一：将图表销毁，然后重新渲染

> 方法二：借助dispatchAction方法，不对图表进行销毁操作

#### 2、地图上方实现悬浮信息的轮播效果

**参考：**

[Echarts官网](https://echarts.apache.org/)

[Echarts主题下载](https://echarts.apache.org/zh/download-theme.html)

[Echarts API](https://echarts.apache.org/zh/option.html)

