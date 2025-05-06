弹窗表单配置
======

Tips

表格中的弹出的表单是内置组件`avue-form`组件,配置属性可以参考[FORM 组件文档](https://v2.avuejs.com/form/form)

默认值
---------------------------------------------------------------------------

配置`value`为字段默认值

```vue
<avue-crud :option="option" :data="data"></avue-crud>

<script>
  export default {
    data() {
      return {
        data: [],
        option: {
          column: [
            {
              label: "姓名",
              prop: "name",
              value: "small",
            },
          ],
        },
      };
    },
  };
</script>
```
打开表单前
-----------------------------------------------------------------------------------------------

Tips

你可以在打开前和关闭前做一些逻辑操作，例如打开根据 id 请求数据，关闭根据 id 保存数据等

打开表单前会执行`beforeOpen`方法，相关返回的方法值可以判断表单当前打开的类型是新增还是编辑

```vue
<avue-crud
  :data="data"
  v-model="form"
  :before-open="beforeOpen"
  :option="option"
></avue-crud>
<script>
  export default {
    data() {
      return {
        form: {},
        data: [
          {
            name: "张三",
            sex: "男",
          },
        ],
        option: {
          column: [
            {
              label: "姓名",
              prop: "name",
            },
            {
              label: "性别",
              prop: "sex",
              type: "select",
              dicData: [
                {
                  label: "男",
                  value: 0,
                },
                {
                  label: "女",
                  value: 1,
                },
              ],
            },
          ],
        },
      };
    },
    methods: {
      beforeOpen(done, type) {
        this.$alert(`我是${type}`, {
          confirmButtonText: "确定",
          callback: (action) => {
            if (["view", "edit"].includes(type)) {
              // 查看和编辑逻辑
            } else {
              //新增逻辑
              this.form.name = "初始化赋值";
              this.form.sex = 0;
            }
            done();
          },
        });
      },
    },
  };
</script>
```
加载数据
-------------------------------------------------------------------------------------

Tips

2.13.1+

打开表单前会执行`beforeOpen`方法，调用`loading`加载等待数据，调用`done`完成加载

```vue
<avue-crud
  :data="data"
  v-model="form"
  :before-open="beforeOpen"
  :option="option"
></avue-crud>
<script>
  export default {
    data() {
      return {
        form: {},
        data: [
          {
            name: "张三",
            sex: "男",
          },
        ],
        option: {
          column: [
            {
              label: "姓名",
              prop: "name",
            },
            {
              label: "性别",
              prop: "sex",
            },
          ],
        },
      };
    },
    methods: {
      beforeOpen(done, type, loading) {
        if (["view", "edit"].includes(type)) {
          loading();
          setTimeout(() => {
            done();
          }, 300);
        } else {
          // 新增逻辑
          this.form.name = "初始化赋值";
          done();
        }
      },
    },
  };
</script>
```
关闭表单前
-----------------------------------------------------------------------------------------------

关闭表单前会执行`beforeClose`方法，执行返回的`done`方法后才会彻底关闭表单

```vue
<avue-crud
  :data="data"
  v-model="form"
  :before-close="beforeClose"
  :option="option"
></avue-crud>
<script>
  export default {
    data() {
      return {
        form: {},
        data: [
          {
            name: "张三",
            sex: "男",
          },
        ],
        option: {
          column: [
            {
              label: "姓名",
              prop: "name",
            },
            {
              label: "性别",
              prop: "sex",
            },
          ],
        },
      };
    },
    methods: {
      beforeClose(done, type) {
        this.$confirm("确认关闭？")
          .then((_) => {
            done();
          })
          .catch((_) => {});
      },
    },
  };
</script>
```
不关弹窗连续添加
-----------------------------------------------------------------------------------------------------------------------------

Tips

源码中涉及自定义卡槽和按钮的操作方法可以下面介绍

*   [自定义按钮](https://v2.avuejs.com/crud/crud-btn-slot.html#%E8%87%AA%E5%AE%9A%E4%B9%89%E5%BC%B9%E7%AA%97%E5%86%85%E6%8C%89%E9%92%AE)
    
*   [按钮方法](https://v2.avuejs.com/crud/crud-fun.html)
    

```vue
<avue-crud
  ref="crud"
  :data="data"
  v-model="form"
  @row-save="rowSave"
  :before-open="beforeOpen"
  :before-close="beforeClose"
  :option="option"
>
  <template slot-scope="{row,index}" slot="menuForm">
    <el-button
      type="primary"
      icon="el-icon-check"
      size="small"
      plain
      v-if="type=='add'"
      @click="handleNext()"
      >继续添加</el-button
    >
  </template>
</avue-crud>

<script>
  export default {
    data() {
      return {
        form: {},
        flag: false,
        type: "",
        data: [],
        option: {
          align: "center",
          menuAlign: "center",
          viewBtn: true,
          column: [
            {
              label: "姓名",
              prop: "name",
            },
            {
              label: "性别",
              prop: "sex",
            },
          ],
        },
      };
    },
    methods: {
      handleNext() {
        this.flag = true;
        this.$refs.crud.rowSave();
      },
      rowSave(form, done, loading) {
        this.data.push(this.deepClone(this.form));
        this.$message.success(JSON.stringify(this.form));
        if (this.flag) {
          this.flag = false;
          loading();
          this.form.name = "";
          this.form.sex = "";
          return;
        }
        done();
      },
      beforeClose(done) {
        this.flag = false;
        done();
      },
      beforeOpen(done, type) {
        this.type = type;
        done();
      },
    },
  };
</script>
```
表单按钮位置
---------------------------------------------------------------------------------------------------------

Tips

2.3.3+

居左 居中 居右

配置`dialogMenuPosition`属性值即可，默认为`right`

```vue
<el-radio-group v-model="direction">
  <el-radio label="left">居左</el-radio>
  <el-radio label="center">居中</el-radio>
  <el-radio label="right">居右</el-radio>
</el-radio-group>
<br /><br />
<avue-crud :option="option" :data="list"></avue-crud>
<script>
  export default {
    watch: {
      direction(value) {
        this.option.dialogMenuPosition = value;
      },
    },
    data() {
      return {
        direction: "right",
        list: [
          {
            id: 1,
            name: "张三",
            sex: 12,
          },
          {
            id: 2,
            name: "李四",
            sex: 12,
          },
        ],
        option: {
          dialogMenuPosition: "right",
          column: [
            {
              label: "id",
              prop: "id",
            },
            {
              label: "姓名",
              prop: "name",
            },
            {
              label: "年龄",
              prop: "sex",
            },
          ],
        },
      };
    },
  };
</script>
```
打开表单方式
---------------------------------------------------------------------------------------------------------

Tips

2.1.0+

从左往右开 从右往左开 从上往下开 从下往上开

配置`dialogType`为弹窗的方式,`dialogDirection`为弹窗的位置

```vue
<el-radio-group v-model="direction">
  <el-radio label="ltr">从左往右开</el-radio>
  <el-radio label="rtl">从右往左开</el-radio>
  <el-radio label="ttb">从上往下开</el-radio>
  <el-radio label="btt">从下往上开</el-radio>
</el-radio-group>
<br /><br />
<avue-crud :option="option" :data="list"></avue-crud>
<script>
  export default {
    watch: {
      direction(value) {
        this.option.dialogDirection = value;
      },
    },
    data() {
      return {
        direction: "rtl",
        list: [
          {
            name: "张三",
            sex: 12,
          },
          {
            name: "李四",
            sex: 12,
          },
        ],
        option: {
          dialogDirection: "rtl",
          dialogType: "drawer",
          column: [
            {
              label: "姓名",
              prop: "name",
            },
            {
              label: "年龄",
              prop: "sex",
            },
          ],
        },
      };
    },
  };
</script>
```
防重提交
-------------------------------------------------------------------------------------

为了防止数据重复提交，加入了防重提交机制，`rowSave`方法和`rowUpdate`方法返回`done`用于关闭表单方法和`loading`用于关闭禁止的表单不关闭表单

```vue
<avue-crud
  :data="data"
  :option="option"
  @row-save="handleRowSave"
  @row-update="handleRowUpdate"
></avue-crud>

<script>
  export default {
    data() {
      return {
        data: [
          {
            name: "张三",
            sex: "男",
          },
          {
            name: "李四",
            sex: "女",
          },
        ],
        option: {
          column: [
            {
              label: "姓名",
              prop: "name",
            },
            {
              label: "性别",
              prop: "sex",
            },
          ],
        },
      };
    },
    methods: {
      handleRowSave(row, done, loading) {
        this.$message.success("1秒后关闭禁止表单");
        setTimeout(() => {
          loading();
          this.$message.success("3秒后关闭表单");
        }, 1000);
        setTimeout(() => {
          done();
        }, 3000);
      },
      handleRowUpdate(row, index, done, loading) {
        this.$message.success("1秒后关闭禁止表单");
        setTimeout(() => {
          loading();
          this.$message.success("3秒后关闭表单");
        }, 1000);
        setTimeout(() => {
          done();
        }, 3000);
      },
    },
  };
</script>
```
标题字段宽度
---------------------------------------------------------------------------------------------------------

`labelWidth`为标题的宽度，默认为`90`，可以配置到`option`下作用于全部,也可以单独配置每一项

```vue
<avue-crud :data="data" :option="option"></avue-crud>

<script>
  export default {
    data() {
      return {
        data: [
          {
            name: "张三",
            sex: "男",
          },
          {
            name: "李四",
            sex: "女",
          },
        ],
        option: {
          labelWidth: 150,
          column: [
            {
              labelWidth: 30,
              label: "姓名",
              prop: "name",
            },
            {
              label: "性别",
              prop: "sex",
            },
          ],
        },
      };
    },
  };
</script>
```
验证
-----------------------------------------------------------------

Tips

具体参考[async-validator (opens new window)](https://github.com/yiminghe/async-validator)

配置验证字段的`rules`的数据对象

```vue
<avue-crud :data="data" :option="option"></avue-crud>

<script>
  export default {
    data() {
      return {
        data: [
          {
            name: "张三",
            sex: "男",
          },
          {
            name: "李四",
            sex: "女",
          },
        ],
        option: {
          column: [
            {
              label: "姓名",
              prop: "name",
              rules: [
                {
                  required: true,
                  message: "请输入姓名",
                  trigger: "blur",
                },
              ],
            },
            {
              label: "性别",
              prop: "sex",
              rules: [
                {
                  required: true,
                  message: "请输入性别",
                  trigger: "blur",
                },
              ],
            },
          ],
        },
      };
    },
  };
</script>
```
自定义验证
-----------------------------------------------------------------------------------------------

Tips

自定义校验 callback 必须被调用。 更多高级用法可参考 [async-validator (opens new window)](https://github.com/yiminghe/async-validator)

```vue
<avue-crud
  :data="data"
  v-model="obj"
  :option="option"
  @error="error"
></avue-crud>

<script>
  export default {
    data() {
      var validatePass = (rule, value, callback) => {
        if (value === "") {
          callback(new Error("请输入密码"));
        } else {
          callback();
        }
      };
      var validatePass2 = (rule, value, callback) => {
        if (value === "") {
          callback(new Error("请再次输入密码"));
        } else if (value !== this.obj.password) {
          callback(new Error("两次输入密码不一致!"));
        } else {
          callback();
        }
      };
      return {
        obj: {},
        data: [],
        option: {
          column: [
            {
              label: "密码",
              prop: "password",
              rules: [
                { required: true, validator: validatePass, trigger: "blur" },
              ],
            },
            {
              label: "确认密码",
              prop: "oldpassword",
              rules: [
                { required: true, validator: validatePass2, trigger: "blur" },
              ],
            },
          ],
        },
      };
    },
    methods: {
      error(err) {
        this.$message.success("请查看控制台");
        console.log(err);
      },
    },
  };
</script>
```
组件对象
-------------------------------------------------------------------------------------

Tips

2.6.2+

打开表单的时候可以获取相关字段的 ref 对象

```vue
<avue-crud
  ref="crud"
  :data="data"
  :before-open="beforeOpen"
  :option="option"
></avue-crud>

<script>
  export default {
    data() {
      return {
        data: [
          {
            text: "测试数据",
          },
        ],
        option: {
          labelWidth: 120,
          column: [
            {
              label: "测试框",
              prop: "text",
            },
          ],
        },
      };
    },
    methods: {
      beforeOpen(done) {
        done();
        setTimeout(() => {
          this.$message.success("查看控制台");
          console.log("text的ref对象");
          console.log(this.$refs.crud.getPropRef("text"));
        }, 0);
      },
    },
  };
</script>
```
字段不同状态
---------------------------------------------------------------------------------------------------------

Tips

2.6.7+

`disabled`、`display`、`detail`等字段在新增和编辑不同状态下，字段的不同状态展示

```vue
<avue-crud :data="data" :option="option"></avue-crud>

<script>
  export default {
    data() {
      return {
        data: [
          {
            name: "张三",
            sex: "男",
            grade: 0,
          },
          {
            name: "李四",
            sex: "女",
            grade: 1,
          },
        ],
        option: {
          column: [
            {
              label: "姓名",
              prop: "name",
              editDisabled: true,
            },
            {
              label: "性别",
              prop: "sex",
              editDisplay: false,
            },
            {
              label: "权限",
              prop: "grade",
              editDetail: true,
              addDisabled: true,
            },
            {
              label: "测试",
              prop: "test",
              addDisplay: false,
            },
          ],
        },
      };
    },
  };
</script>
```
深结构绑定
-----------------------------------------------------------------------------------------------

Tips

2.6.11+

`bing`绑定深层次的结构对象，`prop`也是需要填写

```vue
<avue-crud :option="option" :data="data" v-model="form">
  <div slot-scope="{}" slot="bindForm">
    <el-button type="primary" size="small" @click="form.deep.deep.deep.value='改变deep.deep.deep.value值'">改变deep.deep.deep.value值</el-button>
    <el-button type="primary" size="small" @click="form.test='改变test值'">改变test值</el-button>
    </br></br>
    {{form}}
  </div>
</avue-crud>

<script>
export default{
  data() {
    return {
      form:{},
      data: [
        {
          deep:{
            deep:{
              deep:{
                value:'我是深结构'
              }
            }
          }
        }
      ],
      option: {
        labelWidth: 120,
        column: [
          {
            label: '深结构',
            prop: 'test',
            bind:'deep.deep.deep.value'
          },{
            label: '',
            prop: 'bind',
            span:24,
            hide:true,
            formslot:true
          }
        ]
      }
    }
  }
}
</script>
```
字段排序
-------------------------------------------------------------------------------------

Tips

2.6.16+

配置`order`的序号可以实现表单和表格字段不同的顺序

```vue
<avue-crud :data="data" :option="option"></avue-crud>

<script>
  export default {
    data() {
      return {
        data: [
          {
            name: "张三",
            sex: "男",
          },
          {
            name: "李四",
            sex: "女",
          },
        ],
        option: {
          column: [
            {
              label: "姓名",
              prop: "name",
            },
            {
              label: "性别",
              prop: "sex",
              order: 1,
            },
          ],
        },
      };
    },
    methods: {},
  };
</script>
```
表单窗口拖拽
---------------------------------------------------------------------------------------------------------

Tips

2.5.3+

Tips

同时已经将拖拽封装成指令，在 el 的原声 dialog 上添加[v-dialogDrag](https://v2.avuejs.com/docs/api.html)即可拖拽

`dialogDrag`设置为`true`即可拖动表单

```vue
<avue-crud :data="data" :option="option"></avue-crud>
<script>
  export default {
    data() {
      return {
        data: [
          {
            name: "张三",
            sex: true,
          },
          {
            name: "李四",
            sex: false,
          },
        ],
        option: {
          dialogDrag: true,
          column: [
            {
              label: "姓名",
              prop: "name",
            },
            {
              label: "性别",
              prop: "sex",
            },
          ],
        },
      };
    },
  };
</script>
```
改变结构配置
---------------------------------------------------------------------------------------------------------

Tips

2.8.12+

```vue
<avue-crud
  :defaults.sync="defaults"
  v-model="form"
  :option="option"
  :data="data"
></avue-crud>
<script>
  export default {
    data() {
      return {
        form: {},
        defaults: {},
        data: [
          {
            text1: 0,
          },
        ],
        option: {
          column: [
            {
              label: "内容1",
              prop: "text1",
              type: "radio",
              dicData: [
                {
                  label: "显示",
                  value: 0,
                },
                {
                  label: "隐藏",
                  value: 1,
                },
              ],
            },
            {
              label: "内容2",
              prop: "text2",
              display: true,
            },
            {
              label: "内容3",
              prop: "text3",
            },
          ],
        },
      };
    },
    watch: {
      "form.text1"(val) {
        if (val == 0) {
          this.defaults.text2.display = true;
          this.defaults.text3.label = "内容3";
        } else {
          this.defaults.text2.display = false;
          this.defaults.text3.label = "有没有发现我变了";
        }
      },
    },
  };
</script>
```
与其它字段交互
-------------------------------------------------------------------------------------------------------------------

Tips

2.8.12+

```vue
<avue-crud :data="data" :option="option" v-model="form"></avue-crud>
<script>
  export default {
    data() {
      return {
        data: [
          {
            text1: 0,
          },
        ],
        form: {},
        option: {
          column: [
            {
              label: "内容1",
              prop: "text1",
              type: "radio",
              dicData: [
                {
                  label: "显示",
                  value: 0,
                },
                {
                  label: "隐藏",
                  value: 1,
                },
              ],
              control: (val, form) => {
                if (val === 0) {
                  return {
                    text2: {
                      display: true,
                    },
                    text3: {
                      label: "内容3",
                    },
                  };
                } else {
                  return {
                    text2: {
                      display: false,
                    },
                    text3: {
                      label: "有没有发现我变了",
                    },
                  };
                }
              },
            },
            {
              label: "内容2",
              prop: "text2",
              display: true,
            },
            {
              label: "内容3",
              prop: "text3",
            },
          ],
        },
      };
    },
  };
</script>
```
表单分组
-------------------------------------------------------------------------------------

Tips

*   [表单分组详细用法](https://v2.avuejs.com/form/form-group.html)
    

```vue
<avue-crud :option="option" v-model="obj" :data="data"></avue-crud>
<script>
  let baseUrl = "https://cli.avuejs.com/api/area";
  export default {
    data() {
      return {
        obj: {
          name: "11",
        },
        data: [
          {
            name: "张三",
            sex: 15,
            province: "110000",
            city: "110100",
            area: "110101",
            checkbox: ["110000"],
          },
        ],
        option: {
          column: [
            {
              label: "姓名",
              prop: "name",
              display: false,
            },
            {
              label: "年龄",
              prop: "sex",
              display: false,
            },
          ],
          group: [
            {
              label: "用户信息",
              prop: "jbxx",
              icon: "el-icon-edit-outline",
              column: [
                {
                  label: "姓名",
                  prop: "name",
                },
                {
                  label: "年龄",
                  prop: "sex",
                },
              ],
            },
            {
              label: "退款申请",
              prop: "tksq",
              icon: "el-icon-view",
              column: [
                {
                  label: "省份",
                  prop: "province",
                  type: "select",
                  props: {
                    label: "name",
                    value: "code",
                  },
                  cascader: ["city"],
                  dicUrl: `${baseUrl}/getProvince`,
                  rules: [
                    {
                      required: true,
                      message: "请选择省份",
                      trigger: "blur",
                    },
                  ],
                },
                {
                  label: "城市",
                  prop: "city",
                  type: "select",
                  cascader: ["area"],
                  props: {
                    label: "name",
                    value: "code",
                  },
                  cascaderIndex: 0,
                  dicUrl: `${baseUrl}/getCity/{{key}}`,
                  rules: [
                    {
                      required: true,
                      message: "请选择城市",
                      trigger: "blur",
                    },
                  ],
                },
                {
                  label: "地区",
                  prop: "area",
                  type: "select",
                  props: {
                    label: "name",
                    value: "code",
                  },
                  cascaderIndex: 0,
                  dicUrl: `${baseUrl}/getArea/{{key}}`,
                  rules: [
                    {
                      required: true,
                      message: "请选择地区",
                      trigger: "blur",
                    },
                  ],
                },
              ],
            },
            {
              label: "用户信息",
              prop: "yhxxs",
              icon: "el-icon-edit-outline",
              column: [
                {
                  label: "测试长度",
                  prop: "len",
                  maxlength: 5,
                },
                {
                  labelWidth: 120,
                  label: "测试自定义",
                  prop: "names",
                  formslot: true,
                },
              ],
            },
          ],
        },
      };
    },
  };
</script>
```
数据过滤
-------------------------------------------------------------------------------------

`filterDic`设置为`true`返回的对象不会包含`$`前缀的字典翻译, `filterNull`设置为`true`返回的对象不会包含空数据的字段

```vue
<avue-crud :key="reload" v-model="form" :option="option" :data="data">
  <template slot="nameForm" slot-scope="{size}">
    <el-button size="small" type="danger" @click="filterDic"
      >过滤数据字典</el-button
    >
    <el-button size="small" type="success" @click="filterNull"
      >过滤空数据</el-button
    >
    <el-button size="small" type="primary" @click="filter">不过滤</el-button>
    <p>{{form}}</p>
    <el-input v-model="form.name" :size="size"></el-input>
  </template>
</avue-crud>

<script>
  export default {
    data() {
      return {
        data: [
          {
            cascader: [0, 1],
            tree: 0,
          },
        ],
        reload: Math.random(),
        form: {},
        option: {
          column: [
            {
              label: "姓名",
              span: 24,
              prop: "name",
            },
            {
              label: "级别",
              prop: "cascader",
              type: "cascader",
              dicData: [
                {
                  label: "一级",
                  value: 0,
                  children: [
                    {
                      label: "一级1",
                      value: 1,
                    },
                    {
                      label: "一级2",
                      value: 2,
                    },
                  ],
                },
              ],
            },
            {
              label: "树型",
              prop: "tree",
              type: "tree",
              dicData: [
                {
                  label: "一级",
                  value: 0,
                  children: [
                    {
                      label: "一级1",
                      value: 1,
                    },
                    {
                      label: "一级2",
                      value: 2,
                    },
                  ],
                },
              ],
            },
          ],
        },
      };
    },
    methods: {
      refresh() {
        this.reload = Math.random();
      },
      filter() {
        this.option.filterDic = false;
        this.option.filterNull = false;
        this.refresh();
      },
      filterDic() {
        this.option.filterDic = true;
        this.refresh();
      },
      filterNull() {
        this.option.filterNull = true;
        this.refresh();
      },
    },
  };
</script>
```
render 渲染表单
---------------------------------------------------------------------------------------------------

Tips

2.12.1+

```vue
<avue-crud :data="data" :option="option" v-model="user"></avue-crud>

<script>
  export default {
    data() {
      return {
        user: {},
        data: [
          {
            name: "张三",
            sex: "男",
          },
          {
            name: "李四",
            sex: "女",
          },
        ],
        option: {
          column: [
            {
              label: "姓名",
              prop: "name",
              renderForm: (h, { row }) => {
                return h(
                  "p",
                  {
                    attrs: { id: "box" },
                    class: { demo: true },
                    style: { color: "pink", lineHeight: "30px" },
                  },
                  row.name || "name"
                );
              },
            },
            {
              label: "性别",
              prop: "sex",
            },
          ],
        },
      };
    },
  };
</script>
```
自定义表单
-----------------------------------------------------------------------------------------------

设置列的属性`formslot`为`true`，在卡槽中指定列的`prop`加上`Form`作为卡槽的名称

```vue
<avue-crud :data="data" :option="option" v-model="user">
  <template slot-scope="{type,disabled}" slot="nameForm">
    <el-tag v-if="type=='add'">新增</el-tag>
    <el-tag v-else-if="type=='edit'">修改</el-tag>
    <el-tag v-else-if="type=='view'">查看</el-tag>
    <el-tag>{{user.name?user.name:'暂时没有内容'}}</el-tag>
    <el-input :disabled="disabled" v-model="user.name"></el-input>
  </template>
</avue-crud>

<script>
  export default {
    data() {
      return {
        user: {},
        data: [
          {
            name: "张三",
            sex: "男",
          },
          {
            name: "李四",
            sex: "女",
          },
        ],
        option: {
          column: [
            {
              label: "姓名",
              prop: "name",
              formslot: true,
              rules: [
                {
                  required: true,
                  message: "请输入姓名",
                  trigger: "blur",
                },
              ],
            },
            {
              label: "性别",
              prop: "sex",
            },
          ],
        },
      };
    },
  };
</script>
```
自定义表单错误提示
---------------------------------------------------------------------------------------------------------------------------------------

设置列的属性`errorslot`为`true`，在卡槽中指定列的`prop`加上`Error`作为卡槽的名称,

```vue
<avue-crud :data="data" :option="option">
  <template slot-scope="{error}" slot="nameError">
    <p style="color:green">自定义提示{{error}}</p>
  </template>
</avue-crud>

<script>
  export default {
    data() {
      return {
        user: {},
        data: [
          {
            sex: "男",
          },
          {
            sex: "女",
          },
        ],
        option: {
          column: [
            {
              label: "姓名",
              prop: "name",
              errorslot: true,
              rules: [
                {
                  required: true,
                  message: "请输入姓名",
                  trigger: "blur",
                },
              ],
            },
            {
              label: "性别",
              prop: "sex",
            },
          ],
        },
      };
    },
  };
</script>
```
自定义表单标题
-------------------------------------------------------------------------------------------------------------------

设置列的属性`labelslot`为`true`，在卡槽中指定列的`prop`加上`Label`作为卡槽的名称,

```vue
<avue-crud :data="data" :option="option">
  <template slot-scope="scope" slot="nameLabel">
    <span>姓名&nbsp;&nbsp;</span>
    <el-tooltip
      class="item"
      effect="dark"
      content="文字提示"
      placement="top-start"
    >
      <i class="el-icon-warning"></i>
    </el-tooltip>
  </template>
</avue-crud>

<script>
  export default {
    data() {
      return {
        data: [
          {
            name: "张三",
            sex: "男",
          },
          {
            name: "李四",
            sex: "女",
          },
        ],
        option: {
          column: [
            {
              label: "姓名",
              prop: "name",
              labelslot: true,
              rules: [
                {
                  required: true,
                  message: "请输入姓名",
                  trigger: "blur",
                },
              ],
            },
            {
              label: "性别",
              prop: "sex",
            },
          ],
        },
      };
    },
  };
</script>
```

[按钮自定义](https://v2.avuejs.com/crud/crud-btn-slot/) [深层结构数据](https://v2.avuejs.com/crud/crud-bind/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)
** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号