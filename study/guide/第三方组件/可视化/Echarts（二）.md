**Echarts常用效果速查（基于echarts3/echarts4）**

如无特殊说明，设置参数均从最顶层开始。

### 一、柱状图（条形图）

#### 1、x轴设置

#### 2、y轴设置

#### 3、series设置

### 二、折线图

#### 1、x轴设置

#### 2、y轴设置

#### 3、series设置

### 三、饼图（环形图）

### 四、地图

#### 1、地图区域颜色 `geo-itemStyle` `geo-regions`

```javascript
"geo": {
    "itemStyle": {
        "normal": {
            "areaColor": "#18609e",
        },
        "emphasis": {
            "areaColor": "#18609e"
        }
    },
    "regions": [
        {
            "name": "黑龙江",
            "itemStyle": {
                "normal": {
                    "areaColor": "#1861a0",
                },
                "emphasis": {
                    "areaColor": "#1861a0"
                }
            },
        },
        {
            "name": "吉林",
            "itemStyle": {
                "normal": {
                    "areaColor": "#1964a5",
                },
                "emphasis": {
                    "areaColor": "#1964a5"
                }
            }
        }
    ]       
}
```

**regions示例：**

```json
[
    {
        "name": "黑龙江",
        "itemStyle": {
            "normal": {
                "areaColor": "#1861a0"
            },
            "emphasis": {
                "areaColor": "#1861a0"
            }
        }
    },
    {
        "name": "吉林",
        "itemStyle": {
            "normal": {
                "areaColor": "#1964a5"
            },
            "emphasis": {
                "areaColor": "#1964a5"
            }
        }
    },
    {
        "name": "辽宁",
        "itemStyle": {
            "normal": {
                "areaColor": "#1e78c6"
            },
            "emphasis": {
                "areaColor": "#1e78c6"
            }
        }
    },
    {
        "name": "福建",
        "itemStyle": {
            "normal": {
                "areaColor": "#1d73be"
            },
            "emphasis": {
                "areaColor": "#1d73be"
            }
        }
    },
    {
        "name": "新疆",
        "itemStyle": {
            "normal": {
                "areaColor": "#18609e"
            },
            "emphasis": {
                "areaColor": "#18609e"
            }
        }
    },
    {
        "name": "西藏",
        "itemStyle": {
            "normal": {
                "areaColor": "#1a6aae"
            },
            "emphasis": {
                "areaColor": "#1a6aae"
            }
        }
    },
    {
        "name": "台湾",
        "itemStyle": {
            "normal": {
                "areaColor": "#a6cff2"
            },
            "emphasis": {
                "areaColor": "#a6cff2"
            }
        }
    },
    {
        "name": "广东",
        "itemStyle": {
            "normal": {
                "areaColor": "#cae2f7"
            },
            "emphasis": {
                "areaColor": "#cae2f7"
            }
        }
    },
    {
        "name": "海南",
        "itemStyle": {
            "normal": {
                "areaColor": "#2f8ee0"
            },
            "emphasis": {
                "areaColor": "#2f8ee0"
            }
        }
    },
    {
        "name": "云南",
        "itemStyle": {
            "normal": {
                "areaColor": "#4097e2"
            },
            "emphasis": {
                "areaColor": "#4097e2"
            }
        }
    },
    {
        "name": "内蒙古",
        "itemStyle": {
            "normal": {
                "areaColor": "#1e79c8"
            },
            "emphasis": {
                "areaColor": "#1e79c8"
            }
        }
    },
    {
        "name": "宁夏",
        "itemStyle": {
            "normal": {
                "areaColor": "#4499e3"
            },
            "emphasis": {
                "areaColor": "#4499e3"
            }
        }
    },
    {
        "name": "四川",
        "itemStyle": {
            "normal": {
                "areaColor": "#1861a0"
            },
            "emphasis": {
                "areaColor": "#1861a0"
            }
        }
    },
    {
         "name": "湖南",
         "itemStyle": {
            "normal": {
                "areaColor": "#deedfa"
            },
            "emphasis": {
                "areaColor": "#deedfa"
            }
         }
    },
    {
        "name": "江西",
        "itemStyle": {
            "normal": {
                "areaColor": "#4fabd7"
            },
            "emphasis": {
                "areaColor": "#4fabd7"
            }
        }
    },
    {
        "name": "江苏",
        "itemStyle": {
            "normal": {
                "areaColor": "#53a1e5"
            },
            "emphasis": {
                "areaColor": "#53a1e5"
            }
        }
    },
    {
        "name": "浙江",
            "itemStyle": {
                "normal": {
                    "areaColor": "#1d73be"
                },
                "emphasis": {
                    "areaColor": "#1d73be"
            }
        }
    },
    {
        "name": "上海",
        "itemStyle": {
            "normal": {
                "areaColor": "#175e9b"
            },
            "emphasis": {
                "areaColor": "#175e9b"
            }
        }
    },
    {
        "name": "广西",
        "itemStyle": {
            "normal": {
                "areaColor": "#86bded"
            },
            "emphasis": {
                "areaColor": "#86bded"
            }
        }
    },
    {
        "name": "河北",
        "itemStyle": {
            "normal": {
                "areaColor": "#2081d4"
            },
            "emphasis": {
                "areaColor": "#2081d4"
            }
        }
    },
    {
        "name": "山西",
        "itemStyle": {
            "normal": {
                "areaColor": "#2b8cdf"
            },
            "emphasis": {
                "areaColor": "#2b8cdf"
            }
        }
    },
    {
        "name": "青海",
        "itemStyle": {
            "normal": {
                "areaColor": "#2284d2"
            },
            "emphasis": {
                "areaColor": "#2284d2"
            }
        }
    },
    {
        "name": "湖北",
        "itemStyle": {
            "normal": {
                "areaColor": "#2080d3"
            },
            "emphasis": {
                "areaColor": "#2080d3"
            }
        }
    },
    {
        "name": "安徽",
        "itemStyle": {
            "normal": {
                "areaColor": "#2284d2"
            },
            "emphasis": {
                "areaColor": "#2284d2"
            }
        }
    },
    {
        "name": "香港",
        "itemStyle": {
            "normal": {
                "areaColor": "#cae2f7"
            },
            "emphasis": {
                "areaColor": "#cae2f7"
            }
        }
    },
    {
        "name": "澳门",
        "itemStyle": {
            "normal": {
                "areaColor": "#cae2f7"
            },
            "emphasis": {
                "areaColor": "#cae2f7"
            }
        }
    },
    {
        "name": "河南",
        "itemStyle": {
            "normal": {
                "areaColor": "#317ac7"
            },
            "emphasis": {
                "areaColor": "#317ac7"
            }
        }
    },
    {
        "name": "山东",
        "itemStyle": {
            "normal": {
                 "areaColor": "#1e79c8"
            },
            "emphasis": {
                "areaColor": "#1e79c8"
            }
        }
    },
    {
        "name": "陕西",
        "itemStyle": {
            "normal": {
                "areaColor": "#1e79c8"
            },
            "emphasis": {
                "areaColor": "#1e79c8"
            }
        }
    },
    {
        "name": "甘肃",
        "itemStyle": {
            "normal": {
                "areaColor": "#1d73be"
            },
            "emphasis": {
                "areaColor": "#1d73be"
            }
        }
    },
    {
        "name": "贵州",
        "itemStyle": {
            "normal": {
                "areaColor": "#1e78c5"
            },
            "emphasis": {
                "areaColor": "#1e78c5"
            }
        }
    },
    {
        "name": "北京",
        "itemStyle": {
            "normal": {
                "areaColor": "#124775"
            },
            "emphasis": {
                "areaColor": "#124775"
            }
        }
    },
    {
        "name": "天津",
        "itemStyle": {
            "normal": {
                "areaColor": "#1e79c9"
            },
            "emphasis": {
                "areaColor": "#1e79c9"
            }
        }
    },
    {
        "name": "重庆",
        "itemStyle": {
            "normal": {
                "areaColor": "#18609e"
            },
            "emphasis": {
                "areaColor": "#18609e"
            }
        }
    }
]
```