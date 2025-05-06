Table表格选择器
==========

基础用法
--------------------------------------------------------------------------------------------

> 内部组件为crud组件，大部分属性参考Crud文档

```vue
<avue-form ref="form" :option="option"  ></avue-form>

<script>
export default{
  data() {
    return {
      option: {
          column: [
            {
              label: '表格选择器',
              prop: 'table',
              type: 'table',
              children: {
                border: true,
                column: [
                  {
                    label: '姓名',
                    width: 120,
                    search:true,
                    searchSpan:24,
                    prop: 'name'
                  }, {
                    label: '性别',
                    prop: 'sex'
                  }
                ],
              },
              formatter: (row) => {
                if(!row.name) return ''
                return row.name + '-' + row.sex
              },
              onLoad: ({ page, value, data }, callback) => {
                //首次加载去查询对应的值
                if (value) {
                  this.$message.success('首次查询' + value)
                  callback({
                    id: '0',
                    name: '张三',
                    sex: '男',
                    age:18
                  })
                  return
                }
                if(data){
                  this.$message.success('搜索查询参数' + JSON.stringify(data))
                }
                if(page){
                  this.$message.success('分页参数' + JSON.stringify(page))
                }
                //分页查询信息
                callback({
                  total: 2,
                  data: [
                    {
                      id: '0',
                      name: '张三',
                      sex: '男',
                      age:18
                    }, {
                      id: '1',
                      name: '李四',
                      sex: '女',
                      disabled:true,
                      age:18
                    }, {
                      id: '2',
                      name: '王五',
                      sex: '女'
                    }
                  ]
                })
              },
              props: {
                disabled:'disabled',
                label: 'name',
                value: 'id'
              }
            }
          ]
      }
    }
  }
}
</script>
```

默认值
----------------------------------------------------------------------------------

`value`属性可以提供一个初始化的默认值

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
          {
            label:'表格选择器',
            prop:'table',
            type:'table',
            value:'0',
            children: {
                border: true,
                column: [
                  {
                    label: '姓名',
                    width: 120,
                    search:true,
                    searchSpan:24,
                    prop: 'name'
                  }, {
                    label: '性别',
                    prop: 'sex'
                  }
                ],
              },
              formatter: (row) => {
                if(!row.name) return ''
                return row.name + '-' + row.sex
              },
              onLoad: ({ page, value, data }, callback) => {
                //首次加载去查询对应的值
                if (value) {
                  this.$message.success('首次查询' + value)
                  callback({
                    id: '0',
                    name: '张三',
                    sex: '男',
                    age:18
                  })
                  return
                }
                if(data){
                  this.$message.success('搜索查询参数' + JSON.stringify(data))
                }
                if(page){
                  this.$message.success('分页参数' + JSON.stringify(page))
                }
                //分页查询信息
                callback({
                  total: 2,
                  data: [
                    {
                      id: '0',
                      name: '张三',
                      sex: '男',
                      age:18
                    }, {
                      id: '1',
                      name: '李四',
                      sex: '女',
                      age:18
                    }
                  ]
                })
              },
              props: {
                label: 'name',
                value: 'id'
              }
          }
        ]
      }
    }
  }
}
</script>
```

禁用状态
--------------------------------------------------------------------------------------------

通过`disabled`属性指定是否禁用

```vue
<avue-form :option="option"></avue-form>

<script>
export default{
  data() {
    return {
      option: {
        column: [
         {
            label:'表格选择器',
            prop:'table',
            type:'table',
            disabled:true
         }
        ]
      }
    }
  }
}
</script>
```

多选
------------------------------------------------------------------------

设置`multiple`属性即可启用多选

```vue
<avue-form :option="option" v-model="form"></avue-form>

<script>
export default{
  data() {
    return {
      form:{
        table: [0, 2]
      },
      option: {
        column: [
         {
            label:'表格选择器',
            prop:'table',
            type:'table',
            multiple: true,
            children: {
                border: true,
                column: [
                  {
                    label: '姓名',
                    width: 120,
                    search:true,
                    searchSpan:24,
                    prop: 'name'
                  }, {
                    label: '性别',
                    prop: 'sex'
                  }
                ],
              },
              formatter: (row) => {
                if (Array.isArray(row)) {
                  return row.map(ele => ele.name + '格式化').join(',')
                } else {
                  return row.name + '格式化'
                }
              },
              onLoad: ({ page, value, data }, callback) => {
                //首次加载去查询对应的值
                if (value) {
                  this.$message.success('首次查询' + value)
                  callback([
                    {
                      id: '0',
                      name: '张三',
                      sex: '男',
                      age:18
                    }, {
                      id: '2',
                      name: '王五',
                      sex: '女'
                    }
                  ])
                  return
                }
                if(data){
                  this.$message.success('搜索查询参数' + JSON.stringify(data))
                }
                if(page){
                  this.$message.success('分页参数' + JSON.stringify(page))
                }
                //分页查询信息
                callback({
                  total: 2,
                  data: [
                    {
                      id: '0',
                      name: '张三',
                      sex: '男',
                      age:18
                    }, {
                      id: '1',
                      name: '李四',
                      sex: '女',
                      disabled:true,
                      age:18
                    }, {
                      id: '2',
                      name: '王五',
                      sex: '女'
                    }
                  ]
                })
              },
              props: {
                disabled:'disabled',
                label: 'name',
                value: 'id'
              }
            }
        ]
      }
    }
  }
}
</script>
```

与其它框交互
----------------------------------------------------------------------------------------------------------------

利用内置的`getPropRef`方法可以获取内部值赋值给其它变量

```vue
<avue-form ref="form" :option="option" v-model="form" ></avue-form>

<script>
export default{
  data() {
    return {
      form: {},
      option: {
          column: [
            {
              label: '表格',
              prop: 'table',
              type: 'table',
              children: {
                border: true,
                column: [
                  {
                    label: '姓名',
                    width: 120,
                    search:true,
                    searchSpan:24,
                    prop: 'name'
                  }, {
                    label: '性别',
                    prop: 'sex'
                  }
                ],
              },
              formatter: (row) => {
                if(!row.name) return ''
                return row.name + '-' + row.sex
              },
              onLoad: ({ page, value, data }, callback) => {
                //首次加载去查询对应的值
                if (value) {
                  this.$message.success('首次查询' + value)
                  callback({
                    id: '0',
                    name: '张三',
                    sex: '男',
                    age:18
                  })
                  return
                }
                if(data){
                  this.$message.success('搜索查询参数' + JSON.stringify(data))
                }
                if(page){
                  this.$message.success('分页参数' + JSON.stringify(page))
                }
                //分页查询信息
                callback({
                  total: 2,
                  data: [
                    {
                      id: '0',
                      name: '张三',
                      sex: '男',
                      age:18
                    }, {
                      id: '1',
                      name: '李四',
                      sex: '女',
                      age:18
                    }
                  ]
                })
              },
              props: {
                label: 'name',
                value: 'id'
              }
            },{
              label:'性别',
              prop:'sex'
            },{
              label:'年龄',
              prop:'age'
            }
          ]
      }
    }
  },
  watch:{
    'form.table'(){
      let table = this.$refs.form.getPropRef('table').$refs.temp
      let active = table.active;
      if(Array.isArray(active)) active = active[0]
      this.form.sex = active.sex;
      this.form.age = active.age;
    }
  }
}
</script>
```

[Icon图标选择器](https://v2.avuejs.com/form/form-input-icon/) [Map坐标选择器](https://v2.avuejs.com/form/form-input-map/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号