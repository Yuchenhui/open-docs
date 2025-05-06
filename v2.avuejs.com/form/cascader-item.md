表单多级联动
======

Tips

2.9.0+以下的老版本使用的属性是cascaderItem

Tips

`cascader`为需要联动的子选择框`prop`值，填写多个就会形成一对多的关系,`key`为上一级传递下来的值，你也可以直接写其他`form`的值

Select多级联动
----------------------------------------------------------------------------------------------------------

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
            dicUrl: `${baseUrl}/getCity/{{key}}`,
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
            dicUrl: `${baseUrl}/getArea/{{key}}`,
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

Select+InputTable多级联动
--------------------------------------------------------------------------------------------------------------------------------

```vue
<avue-form :option="option" v-model="form"></avue-form>
<script>
var baseUrl = 'https://cli.avuejs.com/api/area'
export default {
  data(){
    return {
       form:{
          province: '110000',
          city: '110100'
       },
       option:{
          column: [ {
            label: '省份',
            prop: 'province',
            type: 'table',
            cascader:['city'],
            children: {
              border: true,
              column: [{
                label: '名称',
                search:true,
                searchSpan:24,
                prop: 'name'
              }],
            },
            formatter: (row) => {
              if(!row.name) return ''
              return row.id + '-' + row.name
            },
            onLoad: ({ page, value,data }, callback) => {
              //首次加载去查询对应的值
              if (value) {
                this.$message.success('首次查询'+value)
                callback({
                  id: '110000',
                  name: '北京市'
                })
                return
              }
              if(data){
                this.$message.success('搜索查询参数'+JSON.stringify(data))
              }
              if(page){
                this.$message.success('分页参数'+JSON.stringify(page))
              }
              //分页查询信息
              callback({
                total: 2,
                data: [{
                  id: '110000',
                  name: '北京市'
                }, {
                  id: '130000',
                  name: '河北省'
                }]
              })
            },
            props: {
              label: 'name',
              value: 'id'
            }
          },
          {
            label: '城市',
            prop: 'city',
            type: 'select',
            props: {
              label: 'name',
              value: 'code'
            },
            dicUrl: `${baseUrl}/getCity/{{key}}`,
            rules: [
              {
                required: true,
                message: '请选择城市',
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

Select+Radio多级联动
----------------------------------------------------------------------------------------------------------------------

```vue
<avue-form :option="option" v-model="form"></avue-form>
<script>
var baseUrl = 'https://cli.avuejs.com/api/area'
export default {
  data(){
    return {
       form:{
          province: '110000',
          city: '110100'
       },
       option:{
          column: [  {
            label: '省份',
            prop: 'province',
            type: 'radio',
            cascader:['city'],
            span:24,
            props:{
              label:'name',
              value:'code'
            },
            dicUrl: `${baseUrl}/getProvince`,
          },
          {
            label: '城市',
            prop: 'city',
            type: 'select',
            props: {
              label: 'name',
              value: 'code'
            },
            dicUrl: `${baseUrl}/getCity/{{key}}`,
            rules: [
              {
                required: true,
                message: '请选择城市',
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

Select+Input多级联动
----------------------------------------------------------------------------------------------------------------------

110000-北京市 130000-河北省

```vue
<el-tag>110000-北京市</el-tag>
<el-tag>130000-河北省</el-tag>
<avue-form :option="option" v-model="form"></avue-form>
<script>
var baseUrl = 'https://cli.avuejs.com/api/area'
export default {
  data(){
    return {
       form:{
          province: '110000',
          city: '110100'
       },
       option:{
          column: [{
            label: '省份',
            prop: 'province',
            cascader:['city'],
          },
          {
            label: '城市',
            prop: 'city',
            type: 'select',
            props: {
              label: 'name',
              value: 'code'
            },
            dicUrl: `${baseUrl}/getCity/{{key}}`,
            rules: [
              {
                required: true,
                message: '请选择城市',
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

传递其他参数
------------------------------------------------------------------------------------------------------------------

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
          params: 'test'
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
            label:'参数',
            prop:'params'
          },
          {
            label: '城市',
            prop: 'city',
            type: 'select',
            props: {
              label: 'name',
              value: 'code'
            },
            dicUrl: `${baseUrl}/getCity/{{key}}?params={{params}}`,
            rules: [
              {
                required: true,
                message: '请选择城市',
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

[表单数据字典](https://v2.avuejs.com/form/form-dic/) [表单数据格式](https://v2.avuejs.com/form/form-data/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号