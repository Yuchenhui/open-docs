Select选择框
=========

Select选择框
=========================================================================================

基础用法
---------------------------------------------------------------------------------------

通过将`type`属性的值指定为`select`,同时配置`dicData`为字典值

```vue
<avue-form :option="option"></avue-form>
<script>
export default {
  data(){
    return {
       option:{
          column: [{
            label: '下拉框',
            prop: 'select',
            type: 'select',
            dicData:[
              { label:'字典1', value:0 },
              { label:'字典2', value:1 }
            ]
          }]
       }
    }
  }
}
</script>
```

默认值
-----------------------------------------------------------------------------

`value`属性可以提供一个初始化的默认值

```vue
<avue-form :option="option"></avue-form>
<script>
export default{
  data() {
    return {
      option: {
        column: [{
          label:'下拉框',
          prop:'select',
          type:'select',
          dicData:[
            { label:'字典1', value:0 },
            { label:'字典2', value:1 }
          ],
          value:0
        }]
      }
    }
  }
}
</script>
```

禁用状态
---------------------------------------------------------------------------------------

通过`disabled`属性指定是否禁用

```vue
<avue-form :option="option"></avue-form>
<script>
export default{
  data() {
    return {
      option: {
        column: [{
          label:'下拉框',
          prop:'select',
          type:'select',
          dicData:[
            { label:'字典1', value:0 },
            { label:'字典2', value:1 }
          ],
          disabled:true
        }]
      }
    }
  }
}
</script>
```

禁用选项
---------------------------------------------------------------------------------------

返回的字典中数据配置`disabled`属性指定是否禁用

```vue
<avue-form :option="option"></avue-form>
<script>
export default{
  data() {
    return {
      option: {
        column: [{
          label:'下拉框',
          prop:'select',
          type:'select',
          dicData:[
            { label:'字典1', value:0, disabled:true },
            { label:'字典2', value:1 }
          ]
        }]
      }
    }
  }
}
</script>
```

可清空
-----------------------------------------------------------------------------

使用`clearable`属性即可得到一个可清空的输入框,默认为`true`

```vue
<avue-form :option="option"></avue-form>
<script>
export default{
  data() {
    return {
      option: {
        column: [{
          label:'下拉框',
          prop:'input',
          type:'select',
          clearable:false,
          dicData:[
            { label:'字典1', value:0 },
            { label:'字典2', value:1 }
          ]
        }]
      }
    }
  }
}
</script>
```

辅助语
-----------------------------------------------------------------------------

配置下拉数据中`desc`字段

```vue
<avue-form :option="option"></avue-form>
<script>
export default {
  data(){
    return {
       option:{
          column: [{
            label: '下拉框',
            prop: 'select',
            type: 'select',
            dicData:[
              { label:'字典1', desc:'字典描述', value:0 },
              { label:'字典2', value:1 }
            ]
          }]
       }
    }
  }
}
</script>
```

字典属性
---------------------------------------------------------------------------------------

> 指定标签文本和值，默认为label和value

配置`props`属性来指定标签文本和值，默认为`label`和`value`

```vue
<avue-form :option="option"></avue-form>
<script>
export default {
  data(){
    return {
       option:{
          column: [{
            label: '下拉框',
            prop: 'select',
            type: 'select',
            props:{
              label:'name',
              value:'code'
            },
            dicData:[
              { name:'字典1', code:0 },
              { name:'字典2', code:1 }
            ]
          }]
       }
    }
  }
}
</script>
```

下拉框样式
-------------------------------------------------------------------------------------------------

```css
.popperClass .el-select-dropdown__item{
  background-color: rgba(0,0,0,.2);
}
```

`popperClass`属性配置样式的`class`名字,字典中`class`属性为单个框下拉样式

```vue
<avue-form :option="option"></avue-form>
<script>
export default{
  data() {
    return {
      option: {
        column: [{
          label:'下拉框',
          prop:'select',
          type:'select',
          popperClass:'popperClass',
          dicData:[
            { label:'字典1', class:'test', value:0 },
            { label:'字典2', value:1 }
          ]
        }]
      }
    }
  }
}
</script>
```

网络字典
---------------------------------------------------------------------------------------

> 更多用法参考[表单数据字典](https://v2.avuejs.com/form/form-dic)

配置`dicUrl`指定后台接口的地址

```vue
<avue-form :option="option"></avue-form>
<script>
export default {
  data(){
    return {
       option:{
          column: [{
            label: '下拉框',
            prop: 'select2',
            type: 'select',
            props: {
              label: 'name',
              value: 'code'
            },
            dicUrl: 'https://cli.avuejs.com/api/area/getProvince'
          }]
       }
    }
  }
}
</script>
```

基础多选
---------------------------------------------------------------------------------------

设置`multiple`属性即可启用多选，此时值为当前选中值所组成的数组。默认情况下选中值会以 Tag 的形式展现，你也可以设置`tags`属性将它们合并为一段文字。`limit`限制选择个数

```vue
<avue-form v-model="form" :option="option"></avue-form>
<script>
const dicData=[
  { label:'字典1', value:0 },
  { label:'字典2', value:1 },
  { label:'字典3', value:2 }
]
export default {
  data(){
    return {
      form:{
        select:[0,1,2]
      },
       option:{
          column: [{
            label: '下拉框',
            prop: 'select',
            type: 'select',
            multiple:true,
            limit:3,
            dicData:dicData
          },{
            label: '下拉框',
            prop: 'select',
            type: 'select',
            multiple:true,
            tags:true,
            limit:3,
            dicData:dicData
          }]
       }
    }
  }
}
</script>
```

创建条目和搜索
---------------------------------------------------------------------------------------------------------------------

使用`allowCreate`属性即可通过在输入框中输入文字来创建新的条目。注意此时`filterable`必须为真

```vue
<avue-form :option="option"></avue-form>
<script>
export default {
  data(){
    return {
       option:{
          column: [{
            label: '创建',
            prop: 'select',
            type: 'select',
            allowCreate:true,
            filterable:true,
            dicData:[
              { label:'字典1', value:0 },
              { label:'字典2', value:1 }
            ]
          }]
       }
    }
  }
}
</script>
```

自定义模板
-------------------------------------------------------------------------------------------------

配置`props`名称加`Type`卡槽开启即可自定义下拉框的内容,`typeformat`配置回显的内容,但是你提交的值还是`value`并不会改变

```vue
<avue-form :option="option" v-model="form" ref="form">
 <template slot="provinceType" slot-scope="{item,value,label}">
      <img src="/images/logo.png" style="width:20px" /> 
      <span>{{ item }}</span>
  </template>
</avue-form>
<script>
export default {
    data() {
      return {
        form: {
          province:'120000'
        },
        option: {
          column: [{
            label: '单选',
            prop: 'province',
            type: 'select',
            props: {
              label: 'name',
              value: 'code'
            },
            dicUrl: 'https://cli.avuejs.com/api/area/getProvince',
            typeformat(item, label, value) {
              return `值:${item[label]}-名:${item[value]}`
            },
            change:(val)=>{
               this.setSelectImg(val)
            },
            rules: [{
                required: true,
                message: '请选择省份',
                trigger: 'blur'
              }]
           }]
        }
    }
  },
  methods:{
    //这里利用修改dom元素去加图标
    setSelectImg(val){
      let province= this.$refs.form.getPropRef('province').$refs.temp;
      province.$el.children[0].children[0].setAttribute("style",`
        background: url('/images/logo.png') no-repeat; 
        background-position: 10px center; 
        background-size: 20px 20px; 
        text-indent: 30px;`);
    }
}
}
</script>
```

多级联动
---------------------------------------------------------------------------------------

Tips

2.9.0+以下的老版本使用的属性是cascaderItem

Tips

[多级联动详细用法](https://v2.avuejs.com/form/form-cascader-item)

`cascader`为需要联动的子选择框`prop`值，填写多个就会形成一对多的关系,`key`为上一级传递下来的值，你也可以直接写其他`form`的值

```vue
<avue-form :option="option" v-model="form"></avue-form>
<script>
var baseUrl = 'https://cli.avuejs.com/api/area'
export default {
  data(){
    return {
       form:{
          province: '110000',
          city: '110100',
          area: '110101'
       },
       option:{
          column: [{
            label: '省份',
            prop: 'province',
            type: 'select',
            props: {
              label: 'name',
              value: 'code'
            },
            cascader: ['city'],
            dicUrl: `${baseUrl}/getProvince`,
            rules: [
              {
                required: true,
                message: '请选择省份',
                trigger: 'blur'
              }
            ]
          },
          {
            label: '城市',
            prop: 'city',
            type: 'select',
            cascader:['area'],
            props: {
              label: 'name',
              value: 'code'
            },
            dicUrl: `${baseUrl}/getCity/{{key}}?province={{province}}`,
            rules: [
              {
                required: true,
                message: '请选择城市',
                trigger: 'blur'
              }
            ]
          },
          {
            label: '地区',
            prop: 'area',
            type: 'select',
            props: {
              label: 'name',
              value: 'code'
            },
            dicUrl: `${baseUrl}/getArea/{{key}}?city={{city}}`,
            rules: [
              {
                required: true,
                message: '请选择地区',
                trigger: 'blur'
              }
            ]
          }]
       }
    }
  }
}
</script>
```

远程搜索
---------------------------------------------------------------------------------------

> 当你的下拉框数据量很大的时候，你可以启动远程搜索

配置`remote`为`true`即可开启远程搜索，其中`dicUrl`中`{{key}}`为用户输入的关键字

```vue
<avue-form :option="option" v-model="form"></avue-form>
<script>
var baseUrl = 'https://cli.avuejs.com/api/area'
export default {
  data(){
    return {
       form:{
        province: '110000',
        province1: '110000,120000,130000,140000',
       },
       option: {
        column: [{
          label: '省份单选',
          prop: 'province',
          type: 'select',
          remote: true,
          props: {
            label: 'name',
            value: 'code'
          },
          dicUrl: `${baseUrl}/getProvince?id={{key}}`,
          rules: [
            {
              required: true,
              message: '请选择省份',
              trigger: 'blur'
            }
          ]
        },{
          label: '省份多选',
          prop: 'province1',
          type: 'select',
          multiple:true,
          remote: true,
          props: {
            label: 'name',
            value: 'code'
          },
          dicUrl: `${baseUrl}/getProvince?id={{key}}`,
          rules: [
            {
              required: true,
              message: '请选择省份',
              trigger: 'blur'
            }
          ]
        }]
      }
    }
  }
}
</script>
```

分组
-------------------------------------------------------------------

配置`group`为`true`即可开启分组模式

```vue
<avue-form :option="option" v-model="obj"></avue-form>
<script>
export default {
    data() {
      return {
        obj: {
         select:'Shanghai'
        },
        option: {
          column: [{
          label: '分组',
          prop: 'select',
          type: 'select',
          group: true,
          dicData: [{
            label: '热门城市',
            groups: [{
              value: 'Shanghai',
              label: '上海',
              desc:'描述'
            }, {
              value: 'Beijing',
              label: '北京'
            }]
          }, {
            label: '城市名',
            groups: [{
              value: 'Chengdu',
              label: '成都'
            }, {
              value: 'Shenzhen',
              label: '深圳'
            }, {
              value: 'Guangzhou',
              label: '广州'
            }, {
              value: 'Dalian',
              label: '大连'
            }]
          }]
          }]
        }
      }
    }
}
</script>
```

拖拽
-------------------------------------------------------------------

```html
<!-- 导入需要的包 （一定要放到index.html中的head标签里） -->
<script src="https://cdn.staticfile.net/Sortable/1.10.0-rc2/Sortable.min.js"></script>
```

配置`drag`为`true`即可开启拖拽模式

```vue
<avue-form :option="option" v-model="obj"></avue-form>
<script>
export default {
    data() {
      return {
        obj: {
         select:['Shanghai','Beijing','Shenzhen']
        },
        option: {
          column: [{
          label: '拖拽',
          prop: 'select',
          type: 'select',
          drag: true,
          multiple: true,
          dicData: [
            { value: 'Shanghai', label: '上海' },
            { value: 'Beijing', label: '北京' },
            { value: 'Shenzhen', label: '深圳' }
          ]
          }]
        }
      }
    }
}
</script>
```

[Number数字输入框](https://v2.avuejs.com/form/form-number/) [Cascader级联选择器](https://v2.avuejs.com/form/form-cascader/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号