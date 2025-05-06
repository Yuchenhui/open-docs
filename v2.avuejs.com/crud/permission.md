权限控制
====

权限控制
===========================================================================================

Tips

2.6.0+

普通用法
-------------------------------------------------------------------------------------------

权限开关

```vue
权限开关
<el-switch :active-value="false" :inactive-value="true" v-model="text" active-color="#13ce66" inactive-color="#ff4949">
</el-switch>
</br></br>
<avue-crud :option="option" :permission="permission" :data="data"></avue-crud>

<script>
export default {
 data() {
      return {
        text: false,
        permission: {},
        option: {
          column: [{
            label: '姓名',
            prop: 'name'
          }, {
            label: '年龄',
            prop: 'sex'
          }]
        },
        data: [{
          id: 1,
          name: '张三',
          sex: 12,
        }, {
          id: 2,
          name: '李四',
          sex: 20,
        }]
      }
    },
    watch: {
      text() {
        if (this.text === true) {
          this.permission = {
            delBtn: false,
            addBtn: false,
            menu: false,
          }
        } else {
          this.permission = {
            delBtn: true,
            addBtn: true,
            menu: true,
          }
        }
      }
    }
}
</script>
```

函数用法
-------------------------------------------------------------------------------------------

```vue
<avue-crud :option="option" :permission="getPermission" :data="data"></avue-crud>
<script>
export default {
 data() {
      return {
        option: {
          column: [{
            label: '姓名',
            prop: 'name'
          }, {
            label: '年龄',
            prop: 'sex'
          }]
        },
        data: [{
          id: 1,
          name: '张三',
          sex: 12,
        }, {
          id: 2,
          name: '李四',
          sex: 20,
        }]
      }
    },
    methods: {
      getPermission(key, row, index){
        if(key==='editBtn' && index==0){
            return false;
        }else if(key==='delBtn' && index==1){
          return false;
        }
         return true;
      }
    }
}
</script>
```

自定义用法
-----------------------------------------------------------------------------------------------------

Tips

* [自定义按钮](https://v2.avuejs.com/crud/crud-btn-slot.html#%E8%87%AA%E5%AE%9A%E4%B9%89%E5%BC%B9%E7%AA%97%E5%86%85%E6%8C%89%E9%92%AE)
* [按钮方法](https://v2.avuejs.com/crud/crud-fun.html)

```vue
<avue-crud :option="option1"  ref="crud" :data="data">
  <div slot="menu" slot-scope="{size,type,row,index}">
    <el-button :type="type" :size="size" icon="el-icon-edit" :disabled="index==0" @click="$refs.crud.rowEdit(row,index)">编辑</el-button>
    <el-button :type="type" :size="size" icon="el-icon-delete">删除</el-button>
  </div>
</avue-crud>
<script>
export default {
 data() {
      return {
        option1: {
          editBtn:false,
          delBtn:false,
          column: [{
            label: '姓名',
            prop: 'name'
          }, {
            label: '年龄',
            prop: 'sex'
          }]
        },
        data: [{
          id: 1,
          name: '张三',
          sex: 12,
        }, {
          id: 2,
          name: '李四',
          sex: 20,
        }]
      }
    },
    methods: {
     
    }
}
</script>
```