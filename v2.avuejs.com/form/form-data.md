表单数据格式
======

数据类型
-------------------------------------------------------------------------------------

- 组件正常接受数据格式为数组[1,2,3,4],而后台返回的类型为字符串1,2,3,4,设置dataType来进行数据转化
- 数据为字符串，字典类型为数字，设置dataType统一数据类型

{ "cascader": "1,2", "province": 120000, "radio": 1, "checkbox": "1,2,3", "selects": "1|2|3" }

有些数据是数组形式的，我们传入字符串是无法识别的，解决数据字典和字段类型不匹配问题,配置`dataType`属性(string / number),`separator`配置分隔符，默认为`,`  

```vue
<avue-form :option="option" v-model="obj" > </avue-form>

<script>
let baseUrl = 'https://cli.avuejs.com/api/area'
export default{
  data() {
      return {
        obj: {
          cascader:'1,2',
          province: 120000,
          radio:1,
          checkbox:'1,2,3',
          selects:'1|2|3'
        },
        option: {
          column: [
            {
              label:'单选',
              prop:'radio',
              type:'radio',
              dataType:'number',
              dicData:[
                { label:'选项1', value:1 },
                { label:'选项2', value:2 },
                { label:'选项3', value:3 }
              ]
            },
            {
              label:'多选',
              prop:'checkbox',
              type:'checkbox',
              dataType:'number',
              dicData:[
                { label:'选项1', value:1 },
                { label:'选项2', value:2 },
                { label:'选项3', value:3 }
              ]
            },
            {
              label:'多选',
              prop:'selects',
              type:'select',
              multiple:true,
              separator:'|',
              dicData:[
                { label:'选项1', value:'1' },
                { label:'选项2', value:'2' },
                { label:'选项3', value:'3' }
              ]
            },
            {
              label: '级联',
              prop: 'cascader',
              type: 'cascader',
              dataType:'string',
              dicData:[
                {
                  label:'级别1',
                  value:1,
                  children:[
                    { label:'级别2', value:2 }
                  ]
                }
              ],
              rules: [
                {
                  required: true,
                  message: '请选择级联',
                  trigger: 'blur'
                }
              ]
            },
            {
              label: '省份',
              prop: 'province',
              type: 'select',
              dataType:'number',
              props: {
                label: 'name',
                value: 'code'
              },
              dicUrl: `${baseUrl}/getProvince`,
              rules: [
                {
                  required: true,
                  message: '请选择省份',
                  trigger: 'blur'
                }
              ]
            }
          ]
        }
      }
    },
}
</script>
```

深层结构数据
---------------------------------------------------------------------------------------------------------

Tips 2.6.11+

改变deep.deep.deep.value值 改变test值  

{ "deep": { "deep": { "deep": { "value": 1 } } } }

`bind`绑定的对象数据是双向的，改变任意一个，另外一个也会改变

```vue
<el-button type="primary" size="small" @click="form.deep.deep.deep.value='改变deep.deep.deep.value值'">改变deep.deep.deep.value值</el-button>
<el-button type="primary" size="small" @click="form.test='改变test值'">改变test值</el-button>
</br></br>
{{form}}
<avue-form :option="option" v-model="form" > </avue-form>

<script>
export default{
  data() {
    return {
      form: { 
        deep:{
          deep:{
            deep:{
              value:1
            }
          }
        }
      },
      option: {
        labelWidth: 120,
        column: [
          {
            label: '我是深结构',
            prop: 'test',
            bind:'deep.deep.deep.value'
          }
        ]
      }
    }
  }
}
</script>
```

数据过滤
-------------------------------------------------------------------------------------

Tips 2.9.3

过滤数据字典 过滤空数据 不过滤

{ "cascader": [ 0, 1 ], "tree": 0 }

`filterDic`设置为`true`返回的对象不会包含`$`前缀的字典翻译, `filterNull`设置为`true`返回的对象不会包含空数据的字段

```vue
<el-button size="small" type="danger" @click="filterDic">过滤数据字典</el-button>
<el-button size="small" type="success" @click="filterNull">过滤空数据</el-button>
<el-button size="small" type="primary" @click="filter">不过滤</el-button>
<p>{{form}}</p>
<avue-form :key="reload" v-model="form" :option="option" ></avue-form>

<script>
export default {
    data() {
      return {
        reload:Math.random(),
        form: {
          cascader:[0,1],
          tree:0
        },
        option:{
          column:[
            {
              label:'姓名',
              prop:'name',
            },
            {
              label:'级别',
              prop:'cascader',
              type:'cascader',
              dicData:[
                {
                  label:'一级',
                  value:0,
                  children:[
                    { label:'一级1', value:1 },
                    { label:'一级2', value:2 }
                  ]
                }
              ],
            },
            {
              label:'树型',
              prop:'tree',
              type:'tree',
              dicData:[
                {
                  label:'一级',
                  value:0,
                  children:[
                    { label:'一级1', value:1 },
                    { label:'一级2', value:2 }
                  ]
                }
              ]
            }
          ]
        }
      }
    },
    methods:{
      refresh(){
        this.reload=Math.random()
      },
      filter(){
        this.option.filterDic=false
        this.option.filterNull=false
        this.refresh()
      },
      filterDic(){
        this.option.filterDic=true
        this.refresh()
      },
      filterNull(){
        this.option.filterNull=true
        this.refresh()
      }
    }
}
</script>
```

清空过滤字段
---------------------------------------------------------------------------------------------------------

Tips 2.9.3

`filterParams`为点击清空按钮，表单不会清除的数据，默认主键`rowKey`是不会清空的，默认为`id`

```vue
<avue-form  v-model="form" :option="option" ></avue-form>

<script>
export default {
    data() {
      return {
        form:{
          name:'smallwei',
          cascader:[0,1],
          tree:0
        },
        option:{
          filterParams:['name'],
          column:[
            {
              label:'姓名',
              prop:'name',
            },
            {
              label:'级别',
              prop:'cascader',
              type:'cascader',
              dicData:[
                {
                  label:'一级',
                  value:0,
                  children:[
                    { label:'一级1', value:1 },
                    { label:'一级2', value:2 }
                  ]
                }
              ],
            },
            {
              label:'树型',
              prop:'tree',
              type:'tree',
              dicData:[
                {
                  label:'一级',
                  value:0,
                  children:[
                    { label:'一级1', value:1 },
                    { label:'一级2', value:2 }
                  ]
                }
              ]
            }
          ]
        }
      }
    }
}
</script>
```

[表单多级联动](https://v2.avuejs.com/form/form-cascader-item/) [表单组件事件](https://v2.avuejs.com/form/form-event/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号