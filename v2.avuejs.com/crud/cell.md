行编辑
===

可以批量对表格编辑和新增等操作

Tips  
如果进行其它操作可以参考[Form组件事件](https://v2.avuejs.com/form/form-event.html)进行联动

普通用法
-------------------------------------------------------------------------------------

配置数据中`$cellEdit`为`true`即可开启首次编辑。`addRowBtn`为行新增按钮，`cellBtn`设置为true则开启行编辑按钮。在配置中将编辑的字段设置`cell`为`true`，增删改查方法和`crud`组件使用一致，`rowKey`为主键的key，如果数据中存在主键，数据才会保存在表格中。

```vue
<avue-crud ref="crud" :option="option" :data="data" @row-update="addUpdate" @row-save="rowSave"  ></avue-crud>
<script>
export default {
  data(){
    return {
       data:[
          {
            id:0,
            sex:1,
            age:18,
            $cellEdit:true
          },
          {
            id:1,
            name:'李四',
            age:18,
            sex:0,
          }
       ],
       option:{
        addBtn:false,
        addRowBtn:true,
        cellBtn:true,
        menuWidth:250,
        column: [
          {
            label:'姓名',
            prop: 'name',
            cell: true,
            rules: [
              {
                required: true,
                message: '请输入姓名',
                trigger: 'blur'
              }
            ]
          },
          {
            label:'性别',
            prop: 'sex',
            type:'select',
            dicData:[
              {
                label:'男',
                value:0
              },
              {
                label:'女',
                value:1
              }
            ],
            cell: true
          },
          {
            label:'年龄',
            prop: 'age',
            slot:true,
            formslot:true,
            dicData:[
              {
                label:'男',
                value:0
              },
              {
                label:'女',
                value:1
              }
            ],
            rules: [
              {
                required: true,
                message: '请输入年龄',
                trigger: 'blur'
              }
            ],
            cell: true
          },
          {
            label:'开关',
            prop: 'switch',
            type:'switch',
            cell: true
          }
        ]
      }
    }
  },
  methods:{
    rowSave(form, done) {
        this.$message.success(
          '新增数据' + JSON.stringify(form)
        )
        done()
     },
    addUpdate(form,index,done,loading){
      this.$message.success('模拟网络请求')
      setTimeout(() => {
        this.$message.success('关闭按钮等待')
        loading()
      }, 1000)
      setTimeout(() => {
        this.$message.success(
          '编辑数据' + JSON.stringify(form) + '数据序号' + index
        )
        done()
      }, 2000)
    }
  }
}
</script>
```

内容自定义
-----------------------------------------------------------------------------------------------

和普通的卡槽用法一致，可以参考[自定义列](https://v2.avuejs.com/crud/crud-column.html#%E8%87%AA%E5%AE%9A%E4%B9%89%E5%88%97)和[自定义表单](https://v2.avuejs.com/crud/crud-form.html#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%A1%A8%E5%8D%95)

```vue
<avue-crud ref="crud" :option="option" :data="data" @row-update="addUpdate" @row-save="rowSave"  @row-click="handleRowClick" >
  <template slot="age" slot-scope="{row}">
   <el-tag>{{row.age}}</el-tag>
  </template>
   <span slot="ageForm" slot-scope="{row,disabled}">
     自定义:<el-input v-model="row.age" :disabled="disabled"></el-input>
  </span>
  <template slot="nameForm" slot-scope="{row,disabled}">
    <el-input v-model="row.name" :disabled="row.$index==2"></el-input>
  </template>
  <template slot="menuLeft">
    <el-button @click="addRow" size="small">添加10条</el-button>
  </template>
   <template slot="menu" slot-scope="{row,index,size,type}">
    <el-button @click="addBreakRow(index)" :size="size" :type="type">向上添加</el-button>
    <el-button @click="addNextRow(index)" :size="size" :type="type">向下添加</el-button>
  </template>
</avue-crud>
<script>
export default {
  data(){
    return {
       data:[
          {
            id:0,
            sex:1,
            age:18,
            $cellEdit:true
          },
          {
            id:1,
            name:'李四',
            age:18,
            sex:0,
          },
          {
            id:1,
            name:'王五',
            age:18,
            sex:0,
            $cellEdit:true
          }
       ],
       option:{
        addBtn:false,
        addRowBtn:true,
        cellBtn:true,
        menuWidth:250,
        column: [
          {
            label:'姓名',
            prop: 'name',
            cell: true,
            rules: [
              {
                required: true,
                message: '请输入姓名',
                trigger: 'blur'
              }
            ]
          },
          {
            label:'性别',
            prop: 'sex',
            type:'select',
            dicData:[
              {
                label:'男',
                value:0
              },
              {
                label:'女',
                value:1
              }
            ],
            cell: true
          },
          {
            label:'年龄',
            prop: 'age',
            slot:true,
            formslot:true,
            dicData:[
              {
                label:'男',
                value:0
              },
              {
                label:'女',
                value:1
              }
            ],
            rules: [
              {
                required: true,
                message: '请输入年龄',
                trigger: 'blur'
              }
            ],
            cell: true
          },
          {
            label:'开关',
            prop: 'switch',
            type:'switch',
            cell: true
          }
        ]
      }
    }
  },
  methods:{
    rowSave(form, done) {
        this.$message.success(
          '新增数据' + JSON.stringify(form)
        )
        done()
     },
    addUpdate(form,index,done,loading){
      this.$message.success('模拟网络请求')
      setTimeout(() => {
        this.$message.success('关闭按钮等待')
        loading()
      }, 1000)
      setTimeout(() => {
        this.$message.success(
          '编辑数据' + JSON.stringify(form) + '数据序号' + index
        )
        done()
      }, 2000)
    },
    addRow() {
      this.$message.success('正在添加，请稍后')
      setTimeout(() => {
        for (let i = 0; i < 10; i++) {
          this.$refs.crud.rowCellAdd({
            name: '',
          });
        }
      }, 500)
    },
    addNextRow(index){
      this.data.splice(index+1,0,{
        $cellEdit:true
      })
    },
    addBreakRow(index){
      this.data.splice(index,0,{
         $cellEdit:true
      })
    },
    handleRowClick(row, event, column) {
        this.$message({
          showClose: true,
          message: '序号' + row.$index,
          type: 'success',
        });
      }
  }
}
</script>
```

按钮自定义
-----------------------------------------------------------------------------------------------

卡槽中的`row.$cellEdit`用来判断当前状态，`cancelBtn`为取消按钮。

```vue
<avue-crud ref="crud" :option="option" :data="data" @row-update="rowUpdate"  @row-save="rowSave"  @row-click="handleRowClick" >
  <template slot-scope="{row,index}" slot="menu">
    <el-button
      type="text"
      size="small"
      :icon="row.$cellEdit?'el-icon-plus':'el-icon-edit'"
      @click="rowCell(row,index)"
      >{{row.$cellEdit?'自定义保存':'自定义修改'}}</el-button>
    <el-button v-if="row.$cellEdit"
      type="text"
      icon="el-icon-cancel"
      size="small"
      @click="$refs.crud.rowCancel(row,index)"
      >取消</el-button>
    
  </template>
</avue-crud>
<script>
export default {
  data(){
    return {
       data:[
          {
            id:0,
            name:'张三',
            sex:1,
            $cellEdit:true
          },
          {
            id:1,
            name:'李四',
            sex:0,
          }
       ],
       option:{
        addBtn:false,
        editBtn:false,
        addRowBtn:true,
        cellBtn:false,
        cancelBtn:false,
        column: [
          {
            label:'姓名',
            prop: 'name',
            cell: true,
            rules: [
              {
                required: true,
                message: '请输入姓名',
                trigger: 'blur'
              }
            ]
          },
          {
            label:'性别',
            prop: 'sex',
            type:'select',
            dicData:[
              {
                label:'男',
                value:0
              },
              {
                label:'女',
                value:1
              }
            ],
            cell: true
          },
          {
            label:'开关',
            prop: 'switch',
            type:'switch',
            cell: true
          }
        ]
      }
    }
  },
  methods:{
     rowCell(row, index) {
        this.$refs.crud.rowCell(row, index)
      },
      rowSave(form, done) {
        this.$message.success(
          '新增数据' + JSON.stringify(form)
        )
        done()
     },
      rowUpdate(form, index, done) {
        this.$message.success(
          '编辑数据' + JSON.stringify(form) + '数据序号' + index
        )
        done()
      },
      handleRowClick(row, event, column) {
        this.$message({
          showClose: true,
          message: '序号' + row.$index,
          type: 'success',
        });
      }
  }
}
</script>
```

多级联动
-------------------------------------------------------------------------------------

Tips  
版本 2.9.0+

```vue
<avue-crud ref="crud" :option="option" :data="data">
</avue-crud>
<script>
let baseUrl = 'https://cli.avuejs.com/api/area'
export default {
  data(){
    return {
      data: [
        {
          id: 1,
          province: '130000',
          city: '130200',
          area: '130202',
          $cellEdit:true
        },
        {
          id: 2,
          province: '110000',
          city: '110100',
          area: '110101',
          $cellEdit:true
        }
      ],
       option:{
          addRowBtn:true,
          addBtn:false,
          cellBtn:true,
          column: [
            {
              label: '省份',
              prop: 'province',
              type: 'select',
              props: {
                label: 'name',
                value: 'code'
              },
              cell: true,
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
              cell: true,
              cascader: ['area'],
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
              cell: true,
              props: {
                label: 'name',
                value: 'code'
              },
              type: 'select',
              dicUrl: `${baseUrl}/getArea/{{key}}`,
              rules: [
                {
                  required: true,
                  message: '请选择地区',
                  trigger: 'blur'
                }
              ]
            }
          ]
      }
    }
  },
  methods:{
    addRow() {
     this.$refs.crud.rowCellAdd({
        id: 3,
        province: '110000',
        $cellEdit:true
      });
    },
  }
}
</script>
```

行单击编辑
-----------------------------------------------------------------------------------------------

调用行单击或双击事件，在调用内部`rowEdit`方法即可

```vue
<avue-crud ref="crud" :data="data" :option="option" @row-click="handleRowClick"></avue-crud>

<script>
export default {
    data() {
      return {
        data: [
          {
            name:'张三',
            sex:'男'
          }, 
          {
            name:'李四',
            sex:'女'
          }
        ],
        option:{
          menu:false,
          dialogType:'drawer',
          dialogWidth:800,
          column:[
             {
              label:'姓名',
              prop:'name'
            }, 
            {
              label:'性别',
              prop:'sex'
            }
          ]
        }
      };
    },
    methods: {
        handleRowClick (row, event, column) {
          this.$refs.crud.rowEdit(row,row.$index);
        },
    }
}
</script>
```

行双击编辑
-----------------------------------------------------------------------------------------------

```vue
<avue-crud ref="crud" :data="data" :option="option" @row-dblclick="handleRowDBLClick"></avue-crud>

<script>
export default {
    data() {
      return {
        data: [
          {
            name:'张三',
            sex:'男'
          }, 
          {
            name:'李四',
            sex:'女'
          }
        ],
        option:{
          menu:false,
          dialogType:'drawer',
          dialogWidth:800,
          column:[
             {
              label:'姓名',
              prop:'name'
            }, 
            {
              label:'性别',
              prop:'sex'
            }
          ]
        }
      }
    },
    methods: {
       handleRowDBLClick (row, event) {
        this.$refs.crud.rowEdit(row,row.$index);
      },
    }
}
</script>
```