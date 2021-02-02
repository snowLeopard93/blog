
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

进度条插件使用`NProgress`：

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

### 四、实现布局

布局使用`ant-design-vue`里的[Layout组件](https://www.antdv.com/components/layout/#Layout)

### 五、实现抽屉效果修改主题


**推荐：**

[Ant Design Vue](https://www.antdv.com/docs/vue/introduce-cn/)