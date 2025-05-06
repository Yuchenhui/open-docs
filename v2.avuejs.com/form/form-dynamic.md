Dynamic子表单
==========

Tips

这里子子表单只能用于简单的场景，复杂的场景可以利用[Form自定义](https://v2.avuejs.com/form/form-slot/)嵌入一个[Crud行编辑](https://v2.avuejs.com/crud/crud-cell)

表格用法
----------------------------------------------------------------------------------------

> 内部组件为crud组件，大部分属性参考Crud文档

添加10条子表单数据  

配置`dynamic`的`children`字段即可

```vue
<el-button @click="addAll" size="small" type="primary">添加10条子表单数据</el-button>
</br></br>
<avue-form :option="option" v-model="form">
 <template slot-scope="{row}" slot="input">
   <el-tag>序号:{{row.$index}}-数据:{{row.input}}</el-tag>
  </template>
</avue-form>
<script>
export default {
  data() {
      return {
        form: {
          dynamic: [{
            input: 1,
            select: 1
          }, {
            input: 2,
            select: 2
          }]
        },
        option: {
          column: [{
            label: '子表单',
            prop: 'dynamic',
            type: 'dynamic',
            span: 24,
            children: {
              align: 'center',
              headerAlign: 'center',
              rowAdd: (done) => {
                this.$message.success('新增回调');
                done({
                  input: '默认值'
                });
              },
              rowDel: (row, done) => {
                this.$message.success('删除回调' + JSON.stringify(row));
                done();
              },
              column: [{
                width: 200,
                label: '输入框',
                prop: "input"
              }, {
                label: '选择框',
                prop: "select",
                type: 'select',
                dicData: [{
                  label: '测试1',
                  value: 1
                }, {
                  label: '测试2',
                  value: 2
                }]
              }]
            }
          }]
        }
      }
  },
  methods: {
    addAll() {
      for (let i = 0; i < 10; i++) {
        this.form.dynamic.push({
          input: 1,
          select: 1
        })
      }
    }
  }
}
</script>
```

表单用法
----------------------------------------------------------------------------------------

> 内部组件为form组件，大部分属性参考Form文档

配置`type`为`form`类型即可转化为表单格式，配置`index`为`false`即可隐藏序号

```vue
<avue-form :option="option" v-model="form">
 <template slot-scope="{row}" slot="input">
   <el-tag>序号:{{row.$index}}-数据:{{row.input}}</el-tag>
  </template>
</avue-form>
<script>
export default {
  data() {
      return {
        form: {
          dynamic: [{
            input: 1,
            select: 1
          }, {
            input: 2,
            select: 2
          }]
        },
        option: {
          column: [{
            label: '子表单',
            prop: 'dynamic',
            type: 'dynamic',
            span: 24,
            children: {
              index: false,
              align: 'center',
              type: 'form',
              headerAlign: 'center',
              rowAdd: (done) => {
                this.$message.success('新增回调');
                done({
                  input: '默认值'
                });
              },
              rowDel: (row, done) => {
                this.$message.success('删除回调' + JSON.stringify(row));
                done();
              },
              column: [{
                width: 200,
                label: '输入框',
                prop: "input"
              }, {
                label: '选择框',
                prop: "select",
                type: 'select',
                dicData: [{
                  label: '测试1',
                  value: 1
                }, {
                  label: '测试2',
                  value: 2
                }]
              }]
            }
          }]
        }
      }
  }
}
</script>
```

父子联动
----------------------------------------------------------------------------------------

```vue
<avue-form :key="reload" :option="option" v-model="form"></avue-form>
<script>
var baseUrl = 'https://cli.avuejs.com/api/area'
export default {
  data() {
      return {
        form: {},
        reload: Math.random(),
      }
    },
    watch: {
      'form.province'() {
          this.reload = Math.random()
      }
    },
    computed: {
      option() {
        return {
          column: [{
            label: '省份',
            prop: 'province',
            type: 'select',
            props: {
              label: 'name',
              value: 'code'
            },
            dicUrl: `${baseUrl}/getProvince`,
            rules: [{
              required: true,
              message: '请选择省份',
              trigger: 'blur'
            }]
          }, {
            label: '子表单',
            prop: 'dynamic',
            type: 'dynamic',
            span: 24,
            children: {
              column: [{
                label: '城市',
                prop: 'city',
                type: 'select',
                props: {
                  label: 'name',
                  value: 'code'
                },
                dicUrl: `${baseUrl}/getCity/` + this.form.province,
                rules: [{
                  required: true,
                  message: '请选择城市',
                  trigger: 'blur'
                }]
              }]
            }
          }]
        }
      }
    }
}
</script>
```

[Array数组框](https://v2.avuejs.com/form/form-array/) [Tree树型选择框](https://v2.avuejs.com/form/form-input-tree/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号