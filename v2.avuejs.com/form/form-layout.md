表单布局
====

Tips

* size
* span
* gutter
* offset
* labelWidth
* labelPosition

以上属性配置到`option`下作用于全部列，优先列中配置属性生效，更多用法可以参考[Element-Layout 布局 (opens new window)](https://element.eleme.cn/#/zh-CN/component/layout) 和[Element-Form 表单 (opens new window)](https://element.eleme.cn/#/zh-CN/component/form)

栏大小
-----------------------------------------------------------------------------

默认 medium small mini

设置`size`属性调节栏的大小，默认为`small`

```vue
<el-row style="margin-bottom:20px">
   <el-radio-group v-model="sizeValue">
    <el-radio label="small">默认</el-radio>
    <el-radio label="medium">medium</el-radio>
    <el-radio label="small">small</el-radio>
    <el-radio label="mini">mini</el-radio>
  </el-radio-group>
</el-row>
<avue-form :option="option"></avue-form>
<script>
export default {
    data() {
      return {
        sizeValue:'small'
      }
    },
    computed: {
       option(){
         return{
          size:this.sizeValue,
          column: [
            {
              label: '姓名',
              prop: 'name'
            },
            {
              label: '性别',
              prop: 'sex'
            },
            {
              label: '年龄',
              prop: 'number',
              type: 'number'
            }
          ]
         }
       }
    }
  }
</script>
```

栏距列数
---------------------------------------------------------------------------------------

设置`span`属性调节栏列数,默认为12

```vue
<avue-form :option="option"></avue-form>
<script>
export default {
  computed:{
    option(){
      return {
        column: [
          {
            label: '姓名',
            prop: 'name',
            span:24
          },
          {
            label: '性别',
            prop: 'sex',
            span:8
          },
          {
            label: '年龄',
            prop: 'number',
            type: 'number',
            span:8
          }
        ]
       }
    }
  }
}
</script>
```

栏距间隔
---------------------------------------------------------------------------------------

设置`gutter`属性调节栏列数,默认为0

```vue
<avue-form :option="option"></avue-form>
<script>
export default {
  computed:{
    option(){
      return {
        gutter:100,
        column: [
          {
            label: '姓名',
            prop: 'name',
          },
          {
            label: '性别',
            prop: 'sex',
          }
        ]
       }
    }
  }
}
</script>
```

分栏偏移
---------------------------------------------------------------------------------------

设置`offset`属性调节栏列数,默认为12

```vue
<avue-form :option="option"></avue-form>
<script>
export default {
  computed:{
    option(){
      return {
        column: [
          {
            label: '姓名',
            prop: 'name',
            span:8
          },
          {
            label: '性别',
            prop: 'sex',
            offset:8,
            span:8
          },
          {
            label: '年龄',
            prop: 'number',
            type: 'number',
            offset:8,
            span:8
          }
        ]
       }
    }
  }
}
</script>
```

栏成行
-----------------------------------------------------------------------------

设置`row`属性栅格后面的内容是否从新的一行开始展示

```vue
<avue-form :option="option"></avue-form>
<script>
export default {
  computed:{
    option(){
      return {
        column: [
          {
            label: '姓名',
            prop: 'name',
            span:8
          },
          {
            label: '性别',
            prop: 'sex',
            span:8,
            row:true
          },
          {
            label: '年龄',
            prop: 'number',
            type: 'number',
            span:8
          }
        ]
       }
    }
  }
}
</script>
```

栏排序
-----------------------------------------------------------------------------

设`order`属性可排序与`column`中顺序不同

```vue
<avue-form :option="option"></avue-form>
<script>
export default {
    data() {
      return {
        option:{
          column:[
             {
              label:'姓名',
              prop:'name'
            }, {
              label:'性别',
              prop:'sex',
              order:1
            }
          ]
        },
      };
    },
    methods: {
    }
}
</script>
```

栏隐藏
-----------------------------------------------------------------------------

设置`display`属性隐藏栏目

```vue
<avue-form :option="option"></avue-form>
<script>
export default {
  computed:{
    option(){
      return {
        column: [
          {
            label: '姓名',
            prop: 'name',
            display:false
          }
        ]
       }
    }
  }
}
</script>
```

标题宽度
---------------------------------------------------------------------------------------

`labelWidth`为标题的宽度，默认为`110`

```vue
<avue-form :option="option"></avue-form>
<script>
export default {
    data() {
      return {
        option:{
          column:[
             {
              labelWidth:200,
              label:'我是一个超级长的标题',
              prop:'name'
            }, {
              label:'性别',
              prop:'sex'
            }
          ]
        },
      }
    }
}
</script>
```

标题位置
---------------------------------------------------------------------------------------

`labelPosition`为标题的位置，默认为`left`

```vue
<avue-form :option="option"></avue-form>
<script>
export default {
    data() {
      return {
        option:{
          labelPosition:'top',
          column:[
             {
              label:'姓名',
              prop:'name'
            }, {
              label:'性别',
              prop:'sex'
            }
          ]
        },
      }
    }
}
</script>
```

标题辅助语
-------------------------------------------------------------------------------------------------

`labelTip`为标题提示的内容,`labelTipPlacement`为标题提示语的方向，默认为`bottom`

```vue
<avue-form :option="option" ></avue-form>
<script>
export default {
  data(){
    return {
       option:{
          column: [
            {
              label: '内容1',
              prop: 'text1',
              labelTip:'我是一个标题提示语'
            },
            {
              label: '内容2',
              prop: 'text2',
              labelTip:'我是一个标题提示语',
              labelTipPlacement:'right'
            }
          ]
       }
    }
  }
}
</script>
```

内容辅助语
-------------------------------------------------------------------------------------------------

`tip`为提示的内容,`tipPlacement`为提示语的方向，默认为`bottom`

```vue
<avue-form :option="option" ></avue-form>
<script>
export default {
  data(){
    return {
       option:{
          column: [
            {
              label: '内容1',
              prop: 'text1',
              tip:'我是一个默认提示语',
            },
            {
              label: '内容2',
              prop: 'text2',
              tip:'我是一个左边提示语',
              tipPlacement:'left',
            }
          ]
       }
    }
  }
}
</script>
```

详情编辑
---------------------------------------------------------------------------------------

`detail`控制是否为详情页

```vue
<el-button @click="handle" style="margin-left: 20px">{{title}}</el-button>
<br /><br />
<avue-form  :option="option" v-model="obj" @submit="submit"></avue-form>
<script>
export default {
    computed: {
      title() {
        return this.option.detail ? '编 辑' : '保 存'
      }
    },
    data() {
      return {
        type: 0,
        obj: {},
        option: {
          detail:true,
          labelWidth:110,
          group: [
            {
              label: '用户信息',
              prop: 'jbxx',
              icon: 'el-icon-edit-outline',
              column: [
                {
                  label: '姓名',
                  prop: 'name',
                  rules: [
                    {
                      required: true,
                      message: '请输入姓名',
                      trigger: 'blur'
                    }
                  ]
                },
                {
                  label: '性别',
                  prop: 'sex',
                }
              ]
            }, {
              label: '退款申请',
              prop: 'tksq',
              icon: 'el-icon-view',
              column: [
                {
                  label: '省份',
                  span:24,
                  prop: 'province',
                  type: 'select',
                  props: {
                    label: 'name',
                    value: 'code'
                  },
                  dicUrl: `https://cli.avuejs.com/api/area/getProvince`,
                  rules: [
                    {
                      required: true,
                      message: '请选择省份',
                      trigger: 'blur'
                    }
                  ]
                },
                {
                  label: '多选',
                  prop: 'checkbox',
                  type: 'checkbox',
                  all:true,
                  props: {
                    label: 'name',
                    value: 'code'
                  },
                  span: 24,
                  dicUrl: 'https://cli.avuejs.com/api/area/getProvince'
                }
              ]
            }, {
              label: '用户信息',
              prop: 'yhxx',
              icon: 'el-icon-edit-outline',
              column: [
                {
                  label: '测试长度',
                  prop: 'len',
                  value:3,
                  maxlength: 5,
                }, {
                  label: '测试自定义',
                  prop: 'lens',
                  value:3,
                  formslot: true
                }
              ]
            }
          ]
        }
      }
    },
    mounted() {
      setTimeout(() => {
        this.obj = {
          name: 'small',
          province: '110000',
          checkbox: ['110000']
        }
      }, 100)
    },
    methods: {
      handle() {
       this.option.detail=!this.option.detail
      },
      submit() {
        this.$message.success(JSON.stringify(this.obj))
      }
    }
}
</script>
```

编辑

```vue
<el-button @click="detail=!detail">{{title}}</el-button>
<br /><br />
<avue-form :option="option" v-model="obj" @submit="submit">
  <template slot="datetime" slot-scope="scope" >
    <span v-if="detail">
      这是我要选择的日期{{datetime[0]}}年{{datetime[1]}}月{{datetime[2]}}日
    </span>
    <el-input v-else v-model="obj.datetime"></el-input>
  </template>
</avue-form>
<script>
export default {
  computed: {
      datetime() {
        return this.obj.datetime.split('-')
      },
      option() {
        return {
          detail: this.detail,
          column: [
            {
              label: '选择日期',
              span: 12,
              prop: 'datetime',
              type: 'datetime',
              format: "yyyy-MM-dd",
              valueFormat: "yyyy-MM-dd"
            },{
              label: '',
              labelWidth: 10,
              prop: 'divider',
              display: !this.detail,
              component: 'elDivider',//ele分割线
              span: 24,
              params: {
                html: '这是一大堆的文字介绍，很长 很长 很长成这是一大堆的文字介绍，很长 很长 很长成这是一大堆的文字介绍，很长 很长 很长成',
                contentPosition: "left",
              }
            }
          ]
        }
      },
      title() {
        return this.detail ? '编辑' : '保存'
      },
    },
    data() {
      return {
        detail: true,
        obj: {
          datetime: '2020-05-01'
        }
      }
    },
    methods: {
      submit() {
        this.$message.success(JSON.stringify(this.obj))
      }
    }
}
</script>
```

分组展示
---------------------------------------------------------------------------------------

> 将表单已分组的形式展示

用法普通的form组件分组用法一样，在`group`中配置结构体即可

```vue
<avue-form :option="option" v-model="form" @submit="handleSubmit" @tab-click="handleTabClick">
  <template slot="group1Header" slot-scope="{column}">
    <svg aria-hidden="true" style="width:30px;height:30px;">
      <use xlink:href="#icon-duanxinguanli"></use>
    </svg>
     {{column.label}}
  </template>
   <template slot="text3" slot-scope="{}">
    <el-input placeholder="自定义" v-model="form.text3"></el-input>
  </template>
</avue-form>
<script>
export default {
  data(){
    return {
       form:{
          text:'文本',
          text1:'文本1',
          text2:'文本2',
          text3:'文本3',
       },
       option:{
          column:[
            {
              label: '内容',
              prop: 'text',
            }
          ],
          group:[
            {
              icon:'el-icon-info',
              label: '分组1',
              collapse:false,
              prop: 'group1',
              column: [
                {
                  label: '内容1',
                  prop: 'text1',
                }
              ]
            },{
              icon:'el-icon-info',
              label: '分组2',
              arrow:false,
              prop: 'group2',
              column: [
                {
                  label: '选项卡2',
                  prop: 'text2',
                }, {
                  label: '选项卡3',
                  prop: 'text3',
                }
              ]
            }
          ]
       }
    }
  },
  methods:{
    handleSubmit(form){
       this.$message.success(JSON.stringify(this.form))
    },
    handleTabClick(event){
      this.$message.success(event);
    }
  }
}
</script>
```

选项卡展示
-------------------------------------------------------------------------------------------------

> 将表单已选项卡的形式展示

转化  

配置`tabs`为true即可开启选项卡

```vue
<el-button @click="tabs=!tabs">转化</el-button><br /><br />
<avue-form @tab-click="handleTabClick" :option="option" v-model="form" @submit="handleSubmit">
  <template slot="group1Header">
    <h4>自定义表头</h4>
  </template>
</avue-form>
<script>
export default {
  data(){
    return {
       tabs:true,
       form:{
          text:'文本',
          text1:'文本1',
          text2:'文本2',
          text3:'文本3',
       },
    }
  },
  computed:{
    option(){
      return {
          tabs:this.tabs,
          tabsActive:2,
          column: [
            {
              label: '内容1',
              prop: 'text1',
            }
          ],
          group:[
            {
              icon:'el-icon-info',
              label: '分组1',
              prop: 'group1',
              column: [
                {
                  label: '内容1',
                  prop: 'text1',
                }
              ]
            },{
              icon:'el-icon-info',
              label: '分组2',
              prop: 'group2',
              column: [
                {
                  label: '选项卡2',
                  prop: 'text2',
                }, {
                  label: '选项卡3',
                  prop: 'text3',
                }
              ]
            }
          ]
       }
    }
  },
  methods:{
    handleSubmit(form){
       this.$message.success(JSON.stringify(this.form))
        setTimeout(() => {
         done()
       },2000)
    },
    handleTabClick(tabs,event){
      this.$message.success('序号为:'+tabs.index)
    }
  }
}
</script>
```

[Object对象形式](https://v2.avuejs.com/form/form-object/) [表单验证](https://v2.avuejs.com/form/form-rules/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号