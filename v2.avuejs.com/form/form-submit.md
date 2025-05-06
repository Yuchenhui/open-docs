表单操作按钮
======

提交按钮
---------------------------------------------------------------------------------------

`submit`方法为表单提交按钮回调

```vue
<avue-form :option="option" v-model="form" @submit="handleSubmit"></avue-form>
<script>
export default {
  data(){
    return {
       form:{},
       option:{
          column: [{
              label: "用户名",
              prop: "username"
          }]
       }
    }
  },
  methods:{
    handleSubmit(form,done){
       this.$message.success('3s后关闭');
       setTimeout(()=>{
          done()
       },3000)
    }
  }
}
</script>
```

清空按钮
---------------------------------------------------------------------------------------

`reset-change`方法为表单清空按钮回调

```vue
<avue-form :option="option" v-model="form" @reset-change="handleReset"></avue-form>
<script>
export default {
  data(){
    return {
       form:{},
       option:{
          column: [{
              label: "用户名",
              prop: "username"
          }]
       }
    }
  },
  methods:{
    handleReset(){
       this.$message.success('清空成功回调');
    }
  }
}
</script>
```

隐藏按钮
---------------------------------------------------------------------------------------

利用`submitBtn`和`emptyBtn`属性去隐藏按钮

```vue
<avue-form :option="option" v-model="form" ></avue-form>
<script>
export default {
  data(){
    return {
       form:{},
       option:{
          submitBtn:false,
          emptyBtn:false,
          column: [{
              label: "用户名",
              prop: "username"
          }]
       }
    }
  }
}
</script>
```

按钮文案
---------------------------------------------------------------------------------------

利用`submitText`和`emptyText`属性去设置按钮文案

```vue
<avue-form :option="option" v-model="form" ></avue-form>
<script>
export default {
  data(){
    return {
       form:{},
       option:{
          submitText:'完成',
          emptyText:'取消',
          column: [{
              label: "用户名",
              prop: "username"
          }]
       }
    }
  }
}
</script>
```

行内按钮
---------------------------------------------------------------------------------------

利用列的`span`属性和`menuSpan`属性达到行内表单

```vue
<avue-form :option="option" > </avue-form>
<script>
export default{
  data() {
    return {
      option: {
        menuSpan:6,
        column: [
          {
            label: '姓名',
            prop: 'name',
            span:6
          },
          {
            label: '年龄',
            prop: 'sex',
            span:6
          }
        ]
      }
    }
  }
}
</script>
```

按钮位置
---------------------------------------------------------------------------------------

利用`menuPosition`属性设置按钮的位置

```vue
<avue-form :option="option" v-model="form" ></avue-form>
<script>
export default {
  data(){
    return {
       form:{},
       option:{
          menuPosition:'right',
          column: [{
              label: "用户名",
              prop: "username"
          }]
       }
    }
  }
}
</script>
```

自定义按钮
---------------------------------------------------------------------------------------

利用`menuForm`插槽去自定义按钮

```vue
<avue-form ref="form" :option="option" v-model="form" @submit="handleSubmit">
   <template slot-scope="{size}" slot="menuForm">
      <el-button type="primary" :size="size" @click="$refs.form.submit()">自定义提交</el-button>
      <el-button  :size="size" @click="$refs.form.resetForm()">自定义清空</el-button>
  </template>
</avue-form>
<script>
export default {
  data(){
    return {
       form:{},
       option:{
          submitBtn:false,
          emptyBtn:false,
          column: [{
              label: "用户名",
              prop: "username"
          }]
       }
    }
  },
  methods:{
    handleSubmit(form,done){
       this.$message.success('3s后关闭');
       setTimeout(()=>{
          done()
       },3000)
    }
  }
}
</script>
```

打印按钮
---------------------------------------------------------------------------------------

> 你可以调用全局[$Print打印方法](https://v2.avuejs.com/default/print)

配置`printBtn`打开表单打印功能

```vue
<avue-form :option="option" v-model="form" @submit="handleSubmit"></avue-form>
<script>
export default {
  data(){
    return {
       form:{},
       option:{
          printBtn:true,
          column: [{
              label: "用户名",
              prop: "username"
          }]
       }
    }
  }
}
</script>
```

模拟数据按钮
---------------------------------------------------------------------------------------

> 一键生成模拟数据方便测试

```html
<!-- 导入需要的包 （一定要放到index.html中的head标签里） -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/Mock.js/1.0.0/mock-min.js"></script>
```

`mock`设置`true`，在列中配置对应的规则即可，当然你可以自己写模拟逻辑，在`mock`写方法，会返回当前表单的数据，最后`return`即可，详情参考如下例子

```vue
<avue-form :option="option" v-model="form"></avue-form>
<script>
var DIC = {
  VAILD: [
    { label: '真', value: 'true' },
    { label: '假', value: 'false' }
  ],
  SEX: [
    { label: '男', value: 0 },
    { label: '女', value: 1 }
  ]
}
export default {
  data(){
    return {
       form:{
          text:'动态内容1'
       },
       option:{
          mockBtn:true,
          column: [
            {
              label: '头像',
              prop: 'video',
              type: 'upload',
              listType: 'picture-img',
              mock: {
                type: 'image'
              },
              span: 24,
            },
            {
              label: "id",
              prop: "id",
              mock: {
                type: 'id',
                uuid: true
              }
            },
            {
              label: "手机号",
              prop: "tel",
              mock: {
                type: 'tel'
              }
            },
            {
              label: "用户名",
              prop: "username",
              mock:{
                type:'name',
                en:true,
              }
            },
            {
              label: "自定义",
              prop: "text2",
              mock: (form) => {
                return '自定义逻辑' + form.name
              },
              span:8
            },
            {
              label: "姓名",
              prop: "name",
              mock:{
                type:'name'
              },
              span:8
            },
            {
              label: "类型",
              prop: "type",
              type: "select",
              dicData: DIC.VAILD,
              span:6,
              mock:{
                type:'dic',
              },
            },
            {
              label: "权限",
              prop: "grade",
              span: 6,
              type: "checkbox",
              dicData: DIC.VAILD,
              mock:{
                type:'dic',
              },
            },
            {
              label: "开关",
              prop: "switch",
              span: 6,
              type: "switch",
              dicData: DIC.SEX,
              mock:{
                type:'dic'
              },
              hide: true,
              row:true,
            },
            {
              label: "性别",
              prop: "sex",
              span: 6,
              type: "radio",
              dicData: DIC.SEX,
              mock:{
                type:'dic'
              }
            },
            {
              label: "数字",
              prop: "number",
              type: 'number',
              span: 6,
              precision:2,
              mock:{
                type:'number',
                max:1,
                min:2,
                precision:2
              },
              min: 0,
              max: 3,
              row:true,
            },
            {
              label: "网站",
              span: 12,
              prop: "url",
              prepend:'http://',
              mock:{
                type:'url',
                header:false,
              },
              append:'com',
              row:true,
            },
            {
              label: "日期",
              prop: "date",
              type: "date",
              span:8,
              format:'yyyy-MM-dd',
              valueFormat:'yyyy-MM-dd',
              mock:{
                type:'datetime',
                format:'yyyy-MM-dd'
              },
            },
            {
              label: "日期时间",
              prop: "datetime",
              type: "datetime",
              span:8,
              format:'yyyy-MM-dd hh:mm:ss',
              valueFormat:'yyyy-MM-dd hh:mm:ss',
              mock:{
                type:'datetime',
                format:'yyyy-MM-dd hh:mm:ss',
                now:true,
              },
            },
            {
              label: "时间",
              prop: "time",
              type: "time",
              span:8,
              format:'hh:mm:ss',
              valueFormat:'hh:mm:ss',
              mock:{
                type:'datetime',
                format:'hh:mm:ss'
              },
            },
            {
              label: "地址",
              span: 24,
              prop: "address",
              mock:{
                type:'county'
              },
            },
            {
              label: "建议",
              span: 24,
              prop: "adit",
              mock:{
                type:'word',
                min:10,
                max:30
              },
            }
          ]
       }
    }
  }
}
</script>
```