表单自定义
=====

表单自定义
===============================================================================================

自定义内容
-----------------------------------------------------------------------------------------------

```vue
<avue-form v-model="form" :option="option">
  <template slot-scope="{disabled,size}" slot="text">
    <div>
      <el-tag>{{form.text ? form.text : '暂时没有内容'}}</el-tag>
      <el-input :disabled="disabled" :size="size" v-model="form.text" placeholder="这里是自定的表单"></el-input>
    </div>
  </template>
</avue-form>

<script>
export default {
  data() {
    return {
      form: {
        text: ''
      },
      option: {
        labelWidth: 120,
        column: [{
          label: '姓名',
          prop: 'text',
          formslot: true,
          rules: [{
            required: true,
            message: "请输入姓名",
            trigger: "blur"
          }]
        }]
      }
    };
  }
}
</script>
```

自定义标题
-----------------------------------------------------------------------------------------------

```vue
<avue-form v-model="form" :option="option">
  <template slot-scope="{}" slot="textLabel">
    <span>姓名&nbsp;&nbsp;</span>
    <el-tooltip class="item" effect="dark" content="文字提示" placement="top-start">
      <i class="el-icon-warning"></i>
    </el-tooltip>
  </template>
</avue-form>

<script>
export default {
  data() {
    return {
      form: {
        text: ''
      },
      option: {
        labelWidth: 120,
        column: [{
          label: '姓名',
          prop: 'text',
          labelslot: true,
          rules: [{
            required: true,
            message: "请输入姓名",
            trigger: "blur"
          }]
        }]
      }
    };
  }
}
</script>
```

自定义错误提示
-----------------------------------------------------------------------------------------------

```vue
<avue-form v-model="form" :option="option">
  <template slot-scope="{error}" slot="textError">
    <p style="color:green">自定义提示{{error}}</p>
  </template>
</avue-form>

<script>
export default {
  data() {
    return {
      form: {
        text: ''
      },
      option: {
        labelWidth: 120,
        column: [{
          label: '姓名',
          prop: 'text',
          errorslot: true,
          rules: [{
            required: true,
            message: "请输入姓名",
            trigger: "blur"
          }]
        }]
      }
    };
  }
}
</script>
```

自定义按钮
-----------------------------------------------------------------------------------------------

```vue
<avue-form ref="form" v-model="form" :option="option">
  <template slot-scope="{row,index,type}" slot="menuFormBefore">
    <el-tag :type="type">提示</el-tag>
  </template>
  <template slot="menuForm">
    <el-button icon="el-icon-user" type="primary" @click="handleSubmit">提 交</el-button>
    <el-button icon="el-icon-delete" @click="handleEmpty">清 空</el-button>
  </template>
</avue-form>

<script>
export default {
  data() {
    return {
      form: {},
      option: {
        emptyBtn: false,
        submitBtn: false,
        column: [{
          label: "用户名",
          prop: "username",
          rules: [{
            required: true,
            message: "请输入用户名",
            trigger: "blur"
          }]
        }]
      }
    }
  },
  methods: {
    handleEmpty() {
      this.$refs.form.resetForm();
    },
    handleSubmit() {
      this.$refs.form.validate((valid, done, msg) => {
        if (valid) {
          this.$message.success(JSON.stringify(this.form));
          setTimeout(() => {
            done()
          }, 2000)
        }
      })
    }
  }
}
</script>
```

自定义样式
-----------------------------------------------------------------------------------------------

Tips: 2.7.1+

```css
.formClassName {
  padding: 0 0 0 55px !important;
  background-color: #409eff;
  color: #fff;
}
```

`className` 属性配置上样式的名字即可：

```vue
<avue-form :option="option" v-model="form"></avue-form>

<script>
export default {
  data() {
    return {
      form: {},
      option: {
        column: [{
          label: '姓名',
          prop: 'name'
        }, {
          label: '性别',
          prop: 'sex',
          labelPosition: 'top',
          span: 24,
          className: 'formClassName'
        }]
      }
    }
  }
}
</script>
```

render渲染
-----------------------------------------------------------------------------------------------

Tips: 2.12.1+

```vue
<avue-form :option="option" v-model="obj"></avue-form>

<script>
export default {
  data() {
    return {
      obj: {},
      option: {
        column: [{
          label: '姓名',
          prop: 'text',
          render: (h, params) => {
            return h('p', {
              attrs: { id: 'box' },
              class: { 'demo': true },
              style: { color: 'pink', lineHeight: '30px' },
            }, 'Hello World Avue')
          }
        }]
      }
    }
  }
}
</script>
```

引入三方组件
-----------------------------------------------------------------------------------------------

```vue
{{obj}}
<avue-form :option="option" v-model="obj"></avue-form>

<script>
export default {
  data() {
    return {
      obj: {},
      option: {
        column: [{
            label: '',
            labelWidth: 40,
            prop: 'divider',
            component: 'elDivider', // ele分割线
            span: 24,
            event: {
              click: () => {
                this.$message.success('点击方法')
              },
            },
            params: {
              html: '<h2 style="color:red">自定义html标签,点我触发方法</h2>',
              contentPosition: "left",
            }
          },
          {
            label: '文本',
            prop: 'text1',
            render: (h, params) => {
              return h('h2', {
                attrs: { id: 'box' },
                class: { 'demo': true },
                style: { color: 'pink', lineHeight: '30px' },
              }, 'Hello World Avue')
            }
          },
          {
            label: '',
            labelWidth: 40,
            prop: 'calendar',
            component: 'elCalendar', // ele日期
            span: 24,
            params: {}
          }
        ]
      }
    }
  }
}
</script>
```

[表单操作按钮](https://v2.avuejs.com/form/form-submit/) [表单数据字典](https://v2.avuejs.com/form/form-dic/)