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