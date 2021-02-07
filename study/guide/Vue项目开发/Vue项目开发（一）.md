
### 一、项目框架搭建

#### 1、创建项目

```
vue create vue-mall
```

基于`vue-cli4`，涉及技术包括`Babel`、`Vue-router`、`Vuex`、`CSS pre-processors（Less）`、`Linter（Prettier）`、`Unit`、`Jest`

![vue-mall-create-1](../../images/Vue项目开发/vue-mall-create-1.png)

#### 2、安装依赖

```
npm i ant-design-vue moment
```

#### 3、启动项目 

```
npm run serve
```

### 二、引入依赖

#### 1、全局引入

`main.js`

```javascript
import Antd from "ant-design-vue";
// import "ant-design-vue/dist/antd.css";
import "ant-design-vue/dist/antd.less";

Vue.use(Antd);
```

#### 2、部分引入

`main.js`

```javascript
import Button from "ant-design-vue/lib/button";
import "ant-design-vue/lib/button/style";

Vue.use(Button);
```

#### 3、`babel`按需加载

**（1）安装`babel-plugin-import`**

```
npm i babel-plugin-import --save
```

**（2）修改`babel.config.js`**

```javascript
module.exports = {
  presets: ["@vue/cli-plugin-babel/preset"],
  plugins: [
    [
      "import",
      { libraryName: "ant-design-vue", libraryDirectory: "es", style: "css" }
    ] // `style: true` 会加载 less 文件
  ]
};
```

**（3）修改部分引入**

`main.js`

```javascript
import { Button } from "ant-design-vue";

Vue.use(Button);
```

### 三、配置路由

#### 1、引入 `VueRouter`

```javascript
import VueRouter from "vue-router";
Vue.use(VueRouter);
```

**注：** 使用`vue-cli`快速创建的vue项目，配置路由的js已经自动生成，路径为`src/router/index.js`

#### 2、定义路由

**（1）定义父子路由**

```javascript
{
    path: "/form/step-form",
    name: "stepForm",
    children: [
        {
            path: "/form/step-form",
            redirect: "/form/step-form/info"
        },
        {
            path: "/form/step-form/info",
            name: "info"
        },
        {
            path: "/form/step-form/confirm",
            name: "confirm",
        },
        {
            path: "/form/step-form/result",
            name: "result"
        }
    ]
}
```

**（2）动态加载组件**

使用如下语法，其中`webpackChunkName`用于动态打包时使用。
 
```javascript
component: () =>
    import(
        /* webpackChunkName: "form" */ "../views/Forms/StepForm/Step3"
    )
}
``` 

**示例：**

```javascript
{
    path: "/form/step-form/result",
    name: "result",
    component: () =>
        import(
            /* webpackChunkName: "form" */ "../views/Forms/StepForm/Step3"
        )
}
```

**（3）静态加载组件**

```javascript
import NotFound from "../views/404";

const routes = [
    {
        path: "*",
        name: "404",
        // route level code-splitting
        // this generates a separate chunk (about.[hash].js) for this route
        // which is lazy-loaded when the route is visited.
        component: NotFound
    }
]
```

**（4）添加页面加载时的进度条效果**

进度条插件使用[NProgress](https://ricostacruz.com/nprogress/)：

```javascript
import NProgress from "nprogress";
import "nprogress/nprogress.css";

router.beforeEach((to, from, next) => {
  if(to.path !== from.path) {
    NProgress.start();
  }
  next();
});

router.afterEach(() => {
  NProgress.done();
});
```

#### 3、示例

**部分代码如下：**

```javascript
const routes = [
  {
    path: "/",
    component: () =>
      import(/* webpackChunkName: "layout" */ "../layouts/BasicLayout"),
    children: [
      {
        path: "/",
        redirect: "/dashboard/analysis"
      },
      {
        path: "/dashboard",
        name: "dashboard",
        component: { render: h => h("router-view") },
        children: [
          {
            path: "/dashboard/analysis",
            name: "analysis",
            component: () =>
              import(
                /* webpackChunkName: "analysis" */ "../views/Dashboard/Analysis"
              )
          }
        ]
      },
      {
        path: "/form",
        name: "form",
        component: { render: h => h("router-view") },
        children: [
          {
            path: "/form/basic-form",
            name: "basicForm",
            component: () =>
              import(/* webpackChunkName: "form" */ "../views/Forms/BasicForm")
          },
          {
            path: "/form/step-form",
            name: "stepForm",
            component: () =>
              import(
                /* webpackChunkName: "form" */ "../views/Forms/StepForm/index"
              ),
            children: [
              {
                path: "/form/step-form",
                redirect: "/form/step-form/info"
              },
              {
                path: "/form/step-form/info",
                name: "info",
                component: () =>
                  import(
                    /* webpackChunkName: "form" */ "../views/Forms/StepForm/Step1"
                  )
              },
              {
                path: "/form/step-form/confirm",
                name: "confirm",
                component: () =>
                  import(
                    /* webpackChunkName: "form" */ "../views/Forms/StepForm/Step2"
                  )
              },
              {
                path: "/form/step-form/result",
                name: "result",
                component: () =>
                  import(
                    /* webpackChunkName: "form" */ "../views/Forms/StepForm/Step3"
                  )
              }
            ]
          }
        ]
      }
    ]
  }
];

const router = new VueRouter({
  mode: "history",
  base: process.env.BASE_URL,
  routes
});
```

### 四、基本布局

布局使用`ant-design-vue`里的[Layout组件](https://www.antdv.com/components/layout/#Layout)

#### 1、拷贝布局

此处使用的是[侧边布局](antdv.com/components/layout-cn/#components-layout-demo-sider)

#### 2、修改布局

**（1）** 依次将 `<a-layout-sider>`、`<a-layout-header>`、`<a-layout-footer>` 里面的内容清空，替换为项目中自己的组件 `SiderMenu`、`Header`、`Footer`

**（2）** 将`<a-layout-sider>`里面的内容清空，替换为 `<router-view>`

**部分代码如下：**

```BasicLayOut.vue
<template>
  <div :class="[`nav-theme-${navTheme}`, `nav-layout-${navLayout}`]">
    <a-layout id="components-layout-demo-side" style="min-height: 100vh">
      <a-layout-sider
              v-if="navLayout === 'left'"
              :theme="navTheme"
              :trigger="null" v-model="collapsed" collapsible>
        <div class="logo">Ant Design Vue Mall</div>
        <SiderMenu />
      </a-layout-sider>
      <a-layout>
        <a-layout-header style="background: #fff; padding: 0">
          <a-icon
            class="trigger"
            :type="collapsed ? 'menu-unfold' : 'menu-fold'"
            @click="collapsed = !collapsed"
          ></a-icon>
          <Header />
        </a-layout-header>
        <a-layout-content style="margin: 0 16px">
          <router-view></router-view>
        </a-layout-content>
        <a-layout-footer style="text-align: center">
          <Footer />
        </a-layout-footer>
      </a-layout>
    </a-layout>
    <SettingDrawer/>
  </div>
</template>
```

### 五、抽屉和主题

抽屉效果使用`ant-design-vue`里的[Drawer抽屉组件](https://www.antdv.com/components/drawer-cn/#components-drawer)

#### 1、拷贝抽屉

此处使用的是[基本抽屉](https://www.antdv.com/components/drawer-cn/#components-drawer-demo-basic)

#### 2、修改抽屉

将`<a-drawer>`里面的内容清空，替换为自己的表单页面

**部分代码如下：**

```SettingDrawer/index.vue
<template>
  <div>
    <a-drawer
      title="Basic Drawer"
      placement="right"
      :closable="false"
      @close="onClose"
      width="500px"
    >
      <div>
        <h2>整体风格定制</h2>
        <a-radio-group
                :value="$route.query.navTheme || 'dark'"
                @change="e => handleSetting('navTheme', e.target.value)">
          <a-radio value="dark">黑色</a-radio>
          <a-radio value="light">白色</a-radio>
        </a-radio-group>
      </div>
      <div>
        <h2>导航模式</h2>
        <a-radio-group
                :value="$route.query.navLayout || 'left'"
                @change="e => handleSetting('navLayout', e.target.value)">
          <a-radio value="left">左侧</a-radio>
          <a-radio value="top">顶部</a-radio>
        </a-radio-group>
      </div>
    </a-drawer>
  </div>
</template>
```

#### 3、设置抽屉的隐藏显示

通过API提供的`handle` 将抽屉直接挂载到dom上，然后通过修改`visible` 实现抽屉的隐藏显示

```SettingDrawer/index.vue
<template>
  <div>
    <a-drawer
      title="Basic Drawer"
      placement="right"
      :closable="false"
      @close="onClose"
      width="500px"
    >
      <template v-slot:handle>
        <div class="handle" @click="visible = !visible">
          <a-icon :type="visible?'close':'setting'"></a-icon>
        </div>
      </template>

      <div>
        <h2>整体风格定制</h2>
        <a-radio-group
                :value="$route.query.navTheme || 'dark'"
                @change="e => handleSetting('navTheme', e.target.value)">
          <a-radio value="dark">黑色</a-radio>
          <a-radio value="light">白色</a-radio>
        </a-radio-group>
      </div>
      <div>
        <h2>导航模式</h2>
        <a-radio-group
                :value="$route.query.navLayout || 'left'"
                @change="e => handleSetting('navLayout', e.target.value)">
          <a-radio value="left">左侧</a-radio>
          <a-radio value="top">顶部</a-radio>
        </a-radio-group>
      </div>
    </a-drawer>
  </div>
</template>
```

#### 4、修改主题

**（1） 监听`<a-radio-group>` 的 `change`，修改url上的参数，丢到`$router`**

**部分代码如下：**

```SettingDrawer/index.vue
<script>
export default {
  data() {
    return {
      visible: false
    };
  },
  methods: {
    onClose() {
      this.visible = false;
    },
    handleSetting(type, value) {
      this.$router.push({query: {...this.$route.query, [type]: value}})
    }
  }
};
</script>
```

**（2）通过计算属性更新主题**

```BasicLayOut.vue
<script>
import Header from "./Header";
import Footer from "./Footer";
import SiderMenu from "./SiderMenu";
import SettingDrawer from '../components/SettingDrawer';

export default {
  name: "BasicLayout",
  data() {
    return {
      collapsed: false
    };
  },
  computed: {
    navTheme() {
      return this.$route.query.navTheme || "dark";
    },
    navLayout() {
      return this.$route.query.navLayout || "left";
    }
  },
  components: {
    Header,
    Footer,
    SiderMenu,
    SettingDrawer
  }
};
</script>
```


**推荐：**

[Ant Design Vue](https://www.antdv.com/docs/vue/introduce-cn/)