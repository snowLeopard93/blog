
### 一、ant-design-vue 表单

#### 1、前置

**（1）引入ant-design-vue Form**

```main.js
import {
  Form,
  Input
} from "ant-design-vue";

Vue.use(Form);
Vue.use(Input);
```

**（2）基本布局**

```BasicForm.vue
<template>
  <div>
    <a-form :layout="formLayout">
      <a-form-item
        label="Field A"
        :label-col="formItemLayout.labelCol"
        :wrapper-col="formItemLayout.wrapperCol"
      >
        <a-input placeholder="input placeholder" />
      </a-form-item>
      <a-form-item
        label="Field B"
        :label-col="formItemLayout.labelCol"
        :wrapper-col="formItemLayout.wrapperCol"
      >
        <a-input placeholder="input placeholder" />
      </a-form-item>
      <a-form-item :wrapper-col="buttonItemLayout.wrapperCol">
        <a-button type="primary">
          Submit
        </a-button>
      </a-form-item>
    </a-form>
  </div>
</template>

<script>
export default {
  name: "BasicForm",
  data() {
    return {
      formLayout: "horizontal"
    };
  },
  computed: {
    formItemLayout() {
      const { formLayout } = this;
      return formLayout === "horizontal"
        ? {
            labelCol: { span: 4 },
            wrapperCol: { span: 14 }
          }
        : {};
    },
    buttonItemLayout() {
      const { formLayout } = this;
      return formLayout === "horizontal"
        ? {
            wrapperCol: { span: 14, offset: 4 }
          }
        : {};
    }
  },
  methods: {
    handleFormLayoutChange(e) {
      this.formLayout = e.target.value;
    }
};
</script>
```

#### 2、文本框

**（1）表单校验**

**注：** `ant-design-vue`的`v-model`有问题，需要使用通过`@change`进行校验。

```BasicForm.vue
<template>
  <div>
    <a-form :layout="formLayout">
      <a-form-item
        label="Field A"
        :label-col="formItemLayout.labelCol"
        :wrapper-col="formItemLayout.wrapperCol"
        :validateStatus="fieldAStatus"
        :help="fieldAHelp"
      >
        <a-input placeholder="input placeholder" @change="handleFieldAChange" />
      </a-form-item>
      <a-form-item
        label="Field B"
        :label-col="formItemLayout.labelCol"
        :wrapper-col="formItemLayout.wrapperCol"
        :validateStatus="fieldBStatus"
        :help="fieldBHelp"
      >
        <a-input placeholder="input placeholder" @change="handleFieldBChange" />
      </a-form-item>
      <a-form-item :wrapper-col="buttonItemLayout.wrapperCol">
        <a-button type="primary">
          Submit
        </a-button>
      </a-form-item>
    </a-form>
  </div>
</template>

<script>
export default {
  name: "BasicForm",
  data() {
    return {
      formLayout: "horizontal",
      fieldAStatus: "",
      fieldAHelp: "",
      fieldBStatus: "",
      fieldBHelp: ""
    };
  },
  computed: {
    formItemLayout() {
      const { formLayout } = this;
      return formLayout === "horizontal"
        ? {
            labelCol: { span: 4 },
            wrapperCol: { span: 14 }
          }
        : {};
    },
    buttonItemLayout() {
      const { formLayout } = this;
      return formLayout === "horizontal"
        ? {
            wrapperCol: { span: 14, offset: 4 }
          }
        : {};
    }
  },
  methods: {
    handleFormLayoutChange(e) {
      this.formLayout = e.target.value;
    },
    handleFieldAChange(e) {
      if (e.target.value.length <= 5) {
        this.fieldAStatus = "error";
        this.fieldAHelp = "必须大于5个字符";
      } else {
        this.fieldAStatus = "";
        this.fieldAHelp = "";
      }
    },
    handleFieldBChange(e) {
      if (e.target.value.length <= 5) {
        this.fieldBStatus = "error";
        this.fieldBHelp = "必须大于5个字符";
      } else {
        this.fieldBStatus = "";
        this.fieldBHelp = "";
      }
    }
  }
};
</script>
```


