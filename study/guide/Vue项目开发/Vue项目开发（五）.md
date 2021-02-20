### 一、图标使用

#### 1、`ant-design-vue`

[ant-design-vue icon](https://www.antdv.com/components/icon-cn/#components-icon-demo-basic)

#### 2、icon-font

```main.js
const IconFont = Icon.createFromIconfontCN({
  scriptUrl: "//at.alicdn.com/t/font_2376320_22s4zik6wfl.js" // 在 iconfont.cn 上生成
});
Vue.component("IconFont", IconFont);
```

```vue
<template>
  <div style="text-align: center;">
    <IconFont type="icon-icon-404" style="font-size: 100px;" />
  </div>
</template>

<script>
import NotFoundImg from "@/assets/images/404.svg";
export default {
  name: "NotFound"
};
</script>
```

#### 3、本地资源（非svg）

```vue
<template>
  <div style="text-align: center;">
    <img :src="NotFoundImg" />
  </div>
</template>
<script>
import NotFoundImg from "@/assets/images/404.svg";
export default {
  name: "NotFound",
  data() {
    return {
      NotFoundImg
    };
  }
};
</script>
```

#### 4、本地资源（svg）

**（1）安装`vue-svg-loader`**

```
npm i vue-svg-loader --save-dev
```

**（2）修改`vue.config.js`**

```vue.config.js
chainWebpack: config => {
    const svgRule = config.module.rule("svg");

    // 清除已有的所有 loader。
    // 如果你不这样做，接下来的 loader 会附加在该规则现有的 loader 之后。
    svgRule.uses.clear();

    // 添加要替换的 loader
    svgRule.use("vue-svg-loader").loader("vue-svg-loader");
  },
```

**（3）修改vue**

```vue
<template>
  <div style="text-align: center;">
    <IconFont type="icon-icon-404" style="font-size: 100px;" />
    <NotFoundSvg />
  </div>
</template>

<script>
import NotFoundSvg from "@/assets/images/404.svg";

export default {
  name: "NotFound",
  components: {
    NotFoundSvg
  }
};
</script>
```

### 二、定制主题

#### 1、修改`vue.config.js`

**（1）将less-loader版本升级到6.0.0**

```
npm i less-loader@6.0.0 --save-dev
```

**（2）修改vue.config.js**

```vue.config.js
module.exports = {
  css: {
    loaderOptions: {
      less: {
        lessOptions: {
          modifyVars: {
            "primary-color": "#1DA57A"
          },
          javascriptEnabled: true
        }
      }
    }
  }
}
```

#### 2、添加.less文件

用来处理抽屉组件的样式。

```SettingDrawer/index.vue
<style lang="less" src="./index.less" />
```

```SettingDrawer/index.less
@import "~ant-design-vue/lib/style/themes/default.less";

.setting-drawer-handle {
  position: absolute;
  top: 240px;
  right: 500px;
  width: 48px;
  height: 48px;
  background: @primary-color;
  color: #fff;
  font-size: 20px;
  text-align: center;
  line-height: 48px;
  border-radius: 3px 0 0 3px;
}
```

#### 3、修改index.html

```index.html
<script>
    window.less = {
        async: false,
        env: 'dev',
        javascriptEnabled: true,
        modifyVars: {
          "primary-color": "#1DA57A"
        }
    };
</script>
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/less.js/2.7.2/less.min.js"></script>
```

**注：** 通过`window.less.modifyVars({"@primary-color": "red"})`动态切换主题不生效，暂未找到原因。