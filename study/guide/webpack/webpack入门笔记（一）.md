### 一、webpack的安装

```
npm install webpack webpack-cli --save-dev
```

### 二、webpakc的基本使用

#### 1、webpack.config.js

**entry：** 打包入口；

**output：** 输出路径；

**rules：** 配置规则，可以将 `webpack` 的 `loader` 写到里面；

```
const path = require('path');

module.exports = {
    entry: './src/index.js',
    output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
    },
    module: {
        rules: [
            // 加载css
            {
                test: /\.css$/,
                use: [
                    'style-loader',
                    'css-loader'
                ]
            },
            // 加载图片
            {
                test: /\.(png|svg|jpg|gif)$/,
                use: [
                    'file-loader'
                ]
            },
            // 加载字体
            {
                test: /\.(woff|woff2|eot|ttf|otf)$/,
                use: [
                    'file-loader'
                ]
            }
        ]
    }
};
```

#### 2、常用命令

**（1）** config：指定不同的`webpack.config.js`

```
webpack --config webpack.dev.config.js
```

### 三、webpack常用loader

#### url-loader

#### babel-loader

#### css-loader

#### style-loader

#### px2rem-loader

#### raw-loader

#### image-webpack-loader


**参考：**

[webpack中文文档](https://www.webpackjs.com/concepts/)