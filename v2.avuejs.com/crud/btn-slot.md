按钮自定义
=====

自定义新增按钮
-----------------------------------------------------------------------------------------------------------------------

这里利用了`menuLeft`卡槽,同时设置`addBtn`为`false`，调用内置的新增打开弹窗方法`rowAdd`

```vue
<avue-crud :data="data" :option="option" ref="crud">
  <template slot-scope="scope" slot="menuLeft">
    <el-button type="danger"
      icon="el-icon-plus"
      size="small"
      @click="$refs.crud.rowAdd()">新增</el-button>
  </template>
</avue-crud>

<script>
export default {
    data() {
      return {
        data:[
          {
            name:'张三',
            sex:'男'
          }, {
            name:'李四',
            sex:'女'
          }
        ],
        option:{
          addBtn:false,
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
      };
    }
}
</script>
```

自定义编辑和删除按钮
-----------------------------------------------------------------------------------------------------------------------------------------------------

这里利用了`menu`卡槽,同时设置`editBtn`和`delBtn`为`false`，调用内置的编辑和删除方法`rowEdit`和`rowDel`,这里需要传入卡槽返回的2个值`{row,index}`当前行的数据和当前行的序号

```vue
<avue-crud :data="data" :option="option" ref="crud">
  <template slot-scope="{row,index}" slot="menu">
     <el-button type="danger"
                     icon="el-icon-edit"
                     size="small"
                     @click="$refs.crud.rowEdit(row,index)">编辑</el-button>
    <el-button type="success"
        icon="el-icon-delete"
        size="small"
        @click="$refs.crud.rowDel(row,index)">删除</el-button>
  </template>
</avue-crud>

<script>
export default {
    data() {
      return {
        data:[
          {
            name:'张三',
            sex:'男'
          }, {
            name:'李四',
            sex:'女'
          }
        ],
        option:{
          delBtn:false,
          editBtn:false,
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
      };
    }
}
</script>
```

自定义查看按钮
-----------------------------------------------------------------------------------------------------------------------

这里利用了`menu`卡槽,调用内置查看方法`rowView`,这里需要传入卡槽返回的2个值`{row,index}`当前行的数据和当前行的序号

```vue
<avue-crud :data="data" :option="option" ref="crud">
  <template slot-scope="{row,index}" slot="menu">
    <el-button type="success"
        icon="el-icon-delete"
        size="small"
        @click="$refs.crud.rowView(row,index)">查看</el-button>
  </template>
</avue-crud>

<script>
export default {
    data() {
      return {
        data:[
          {
            name:'张三',
            sex:'男'
          }, {
            name:'李四',
            sex:'女'
          }
        ],
        option:{
          delBtn:false,
          editBtn:false,
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
      };
    }
}
</script>
```

自定义弹窗内按钮
---------------------------------------------------------------------------------------------------------------------------------

新增和更新按钮要根据返回的`type`值判断，在`menuForm`卡槽中自定义按钮，调用内置方法即可

```vue
<avue-crud :data="data" :option="option" ref="crud">
  <template slot-scope="{row,index,type}" slot="menuFormBefore">
    <el-tag :type="type">提示</el-tag>
  </template>
   <template slot-scope="{row,index,type}" slot="menuForm">
    <el-button type="primary"
                     icon="el-icon-check"
                     size="small"
                     v-if="type=='add'"
                     @click="$refs.crud.rowSave()"
                    >自定义新增</el-button>
    <el-button type="primary"
                     icon="el-icon-check"
                     size="small"
                    v-if="type=='edit'"
                     @click="$refs.crud.rowUpdate()"
                    >自定义修改</el-button>
   <el-button type="primary"
                     icon="el-icon-check"
                     size="small"
                     @click="$refs.crud.closeDialog()"
                    >取消</el-button>
  </template>
</avue-crud>

<script>
export default {
    data() {
      return {
        data:[
          {
            name:'张三',
            sex:'男'
          }, {
            name:'李四',
            sex:'女'
          }
        ],
        option:{
          saveBtn:false,
          updateBtn:false,
          cancelBtn:false,
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
      };
    }
}
</script>
```

[按钮文案和图标](https://v2.avuejs.com/crud/crud-text/) [弹窗表单配置](https://v2.avuejs.com/crud/crud-form/)