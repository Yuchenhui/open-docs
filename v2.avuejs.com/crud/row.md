表格行配置项
======

边框
----------------------------------------------------------------
默认情况下，是不具有竖直方向的边框的，如果需要，可以使用`border`属性，它接受一个`Boolean`，设置为`true`即可启用。

```vue
<avue-crud :data="data" :option="option" ></avue-crud>

<script>
export default {
    data() {
      return {
        data:[
          {
            name:'张三',
            sex:'男'
          },{
            name:'李四',
            sex:'女'
          }
        ],
        option:{
          border:true,
          align:'center',
          menuAlign:'center',
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

条纹
----------------------------------------------------------------
默认情况下，是不具有行彩色条纹的，如果需要，可以使用`stripe`属性，它接受一个`Boolean`，设置为`true`即可启用。

```vue
<avue-crud :data="data" :option="option1" ></avue-crud>

<script>
export default {
    data() {
      return {
        data:[
          {
            name:'张三',
            sex:'男'
          },{
            name:'李四',
            sex:'女'
          }
        ],
        option1:{
          stripe:true,
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

行和单元格样式
---------------------------------------------------------------------------------
开放了`cell-style`和`row-style`方法

```vue
<avue-crud :data="data" :option="option" :cell-style="cellStyle" :row-style="rowStyle"></avue-crud>

<script>
export default {
    data() {
      return {
        data:[
          {
            name:'张三',
            money:3000
          }, {
            name:'李四',
            sex:false,
            money:4000
          }, {
            name:'王五',
            sex:false,
            money:2000
          }
        ],
        option:{
          column:[
             {
              label:'姓名',
              prop:'name'
            },{
              label:'工资',
              prop:'money'
            }
          ]
        }
      };
    },
    methods: {
      rowStyle({row,column,rowIndex}){
        if(rowIndex%2===0){
          return {
              backgroundColor:'#eee',
              color:'#fff'
          }
        }
      },
      cellStyle({row,column,rowIndex,columnIndex}){
        if(columnIndex==1){
          if(row.money<=3000){
            return {
              color:'green',
              fontWeight:'bold',
              fontSize:'20'
            }
          }else{
            return {
              color:'red',
              fontWeight:'bold',
              fontSize:'20'
            }
          }
        }
      }
    }
}
</script>
```

自定义行样式
---------------------------------------------------------------------------------
```css
.warning-row{
  background-color: #F56C6C !important;
  color:#fff;
}
.success-row{
  background-color: #67C23A !important;
  color:#fff;
}
.warning-row.hover-row td,.success-row.hover-row td{
  background-color: initial !important;
}
```

可以通过指定组件的`row-class-name`属性来为crud中的某一行添加class，表明该行处于某种状态，返回当前行的`row`数据和行的序号`index`

```vue
<avue-crud :data="data" :option="option"  :row-class-name="tableRowClassName"></avue-crud>

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
    },
    methods: {
      tableRowClassName ({ row, rowIndex }) {
        if (rowIndex === 0) {
          return 'warning-row';
        } else if (rowIndex === 1) {
          return 'success-row';
        }
        return '';
      }
    }
}
</script>
```

行多选
--------------------------------------------------------------------------
设`selection`属性为`true`即可；勾选的同时会回调`selectionChange`方法返回当前选中的数据，`toggleRowSelection`方法设置行勾选，`toggleAllSelection`方法设置全部勾选。

```vue
<avue-crud ref="crud" :data="data" :option="option" @selection-change="selectionChange">
   <template slot="menuLeft" slot-scope="{size}">
    <el-button type="success" icon="el-icon-check" :size="size" @click="toggleAllSelection()">选中全部</el-button>
    <el-button type="success" icon="el-icon-check" :size="size" @click="toggleRowSelection(data[0])">选中第一行</el-button>
    <el-button type="success" icon="el-icon-check" :size="size" @click="toggleSelection([data[1]])">选中第二行</el-button>
    <el-button type="danger" icon="el-icon-delete" :size="size" @click="toggleSelection()">取消选择</el-button>
  </template>
</avue-crud>

<script>
export default {
    data() {
      return {
        data: [
          {
            id:1,
            name: '张三',
            sex: '男'
          },{
            id:2,
            name: '李四',
            sex: '女'
          }
        ],
        option:{
          selection: true,
          align:'center',
          menuAlign:'center',
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
    },
    methods: {
      selectionChange(list){
        this.$message.success('选中的数据'+ JSON.stringify(list));
      },
      toggleAllSelection(){
        this.$refs.crud.$refs.table.toggleAllSelection()
      },
      toggleSelection(data){
        //传递数组进去，会勾选数组中的对象，如果已经勾选则会取消勾选
        this.$refs.crud.toggleSelection(data);
      },
      toggleRowSelection(row){
        //第一个参数为数据，第二个参数为是否勾选
        this.$refs.crud.toggleRowSelection(row,true);
      }
    }
}
</script>
```

禁止某个项选择
---------------------------------------------------------------------------------
`selectable`函数决定该行是否可以勾选

```vue
<avue-crud ref="crud" :data="data" :option="option" @selection-change="selectionChange" ></avue-crud>
<script>
export default {
    data() {
      return {
        data: [
          {
            id:1,
            name: '张三',
            sex: '男'
          },{
            id:2,
            name: '李四',
            sex: '女'
          }
        ],
        option:{
          selection: true,
          selectable:(row,index)=>{
            return index===1;
          },
          tip:false,
          align:'center',
          menuAlign:'center',
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
    },
    methods: {
      selectionChange(list){
        this.$message.success('选中的数据'+ JSON.stringify(list));
      }
    }
}
</script>
```

翻页多选
------------------------------------------------------------------------------------
设置`reserveSelection`为`true`保留之前的勾选

```vue
<avue-crud  :page.sync="page" :data="data" :option="option" @selection-change="selectionChange" @on-load="onLoad">
</avue-crud>

<script>
export default {
    data() {
      return {
         page: {
          pageSize: 2,
          pageSizes:[2]
        },
        data: [],
        option:{
          selection: true,
          reserveSelection:true,
          align:'center',
          menuAlign:'center',
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
    },
    methods: {
      onLoad(page) {
        this.page.total = 4
        //模拟分页
        if (this.page.currentPage === 1) {
          this.data = [
            {
              id:1,
              name: '张三',
              sex: '男'
            },{
              id:2,
              name: '李四',
              sex: '女'
            }
          ]
        } else if (this.page.currentPage == 2) {
          this.data = [
            {
              id:3,
              name: '王五',
              sex: '女'
            },{
              id:4,
              name: '赵六',
              sex: '女'
            }
          ]
        }
      },
      selectionChange(list){
        this.$message.success('选中的数据'+ JSON.stringify(list));
      }
    }
}
</script>
```

多选提示
------------------------------------------------------------------------------------
设置`tip`为`false`可以取消表格上方显示的提示，同时支持对应的卡槽自定义

```vue
<avue-crud ref="crud" :data="data" :option="option" @selection-change="selectionChange">
   <template slot="tip">
    <el-tag type="danger" size="mini">自定义内容</el-tag>
  </template>
</avue-crud>

<script>
export default {
    data() {
      return {
        data: [
          {
            id:1,
            name: '张三',
            sex: '男'
          },{
            id:2,
            name: '李四',
            sex: '女'
          }
        ],
        option:{
          selection: true,
          align:'center',
          menuAlign:'center',
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

行单选
--------------------------------------------------------------------------
选中第二行 取消选择

单选一行数据时需要设置`highlightCurrentRow`属性为`true`，回调`current-row-change`方法，同时返回当前行的`row`数据

```vue
<avue-crud ref="crud" :data="data" :option="option0" @current-row-change="handleCurrentRowChange"></avue-crud>
<div style="margin-top: 20px">
    <el-button @click="setCurrent(data[1])">选中第二行</el-button>
    <el-button @click="setCurrent()">取消选择</el-button>
</div>

<script>
export default {
    data() {
      return {
        data: [
          {
            name:'张三',
            sex:'男'
          }, {
            name:'李四',
            sex:'女'
          }
        ],
        option0:{
          highlightCurrentRow:true,
          column:[
             {
              label:'姓名',
              prop:'name'
            }, {
              label:'性别',
              prop:'sex'
            }
          ]
        }
      }
    },
    methods: {
        setCurrent(row) {
          this.$refs.crud.setCurrentRow(row);
        },
        handleCurrentRowChange(val){
          this.$notify({
            showClose: true,
            message: '单选'+JSON.stringify(val),
            type: 'success',
          });
        }
    }
}
</script>
```

行单选(利用卡槽)
-------------------------------------------------------------------------------------
这里利用了列自定义卡槽方式去实现行单选

```vue
<avue-crud ref="crud" :data="data" :option="option" @row-click="rowClick">
  <template slot="radio"
              slot-scope="{row}">
      <el-radio v-model="selectRow"
                :label="row.$index">-</el-radio>
    </template>
</avue-crud>

<script>
export default {
    data() {
      return {
        selectRow: '',
        data: [
          {
            id:1,
            name: '张三',
            sex: '男'
          },{
            id:2,
            name: '李四',
            sex: '女'
          }
        ],
        option:{
          align:'center',
          menuAlign:'center',
          column:[{
              label: '',
              prop: 'radio',
              width: 60,
              hide: false
            },
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
    },
    methods:{
      rowClick (row) {
        this.selectRow = row.$index
        this.$message.success('选择序号'+row.$index)
      },
    }
}
</script>
```

展开行
--------------------------------------------------------------------------
Tips 1.0.8+

使用`expand`属性时必须配置`rowKey`属性为你行数据的主键，不能重复，`defaultExpandAll`属性默认展开全部，`expandRowKeys`为展开指定`rowKey`主键的数组，同时你也可以调用`toggleRowExpansion`方法传入你要展开的行。

```vue
<avue-crud ref="crud" :option="option" :data="data" @expand-change="expandChange">
  <template slot="expand" slot-scope="{row}">
    {{row}}
  </template>
</avue-crud>

<script>
export default {
 data() {
    return {
      option: {
        expand: true,
        expandRowKeys:[1],
        rowKey:'id',
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
  }, methods: {
    expandChange(row, expendList) {
      this.$message.success('展开回调')
    },
  }
}
</script>
```

展开行(手风琴模式)
-------------------------------------------------------------------------------------
`expand-change`配置`expandRowKeys`去使用

```vue
<avue-crud ref="crud" :option="option1" :data="data" @expand-change="expandChanges">
  <template slot="expand" slot-scope="{row}">
    {{row}}
  </template>
</avue-crud>

<script>
export default {
 data() {
    return {
      option1:{
        expand: true,
        expandRowKeys:[],
        rowKey:'id',
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
   expandChanges(row, expendList) {
      if (expendList.length) {
        this.option1.expandRowKeys = []
        if (row) {
          this.option1.expandRowKeys.push(row.id)
        }
      } else {
        this.option1.expandRowKeys = []
      }
      this.$message.success('展开回调')
    }
  }
}
</script>
```

行单击方法
----------------------------------------------------------------------------------------------
单击一行数据时回调`row-click`方法，同时返回当前行的`row`数据，`event`当前的操作对象，`column`当前列的属性

```vue
<avue-crud :data="data" :option="option" @row-click="handleRowClick"></avue-crud>

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
          column:[
             {
              label:'姓名',
              prop:'name'
            }, {
              label:'性别',
              prop:'sex'
            }
          ]
        }
      };
    },
    methods: {
        handleRowClick (row, event, column) {
          this.$notify({
            showClose: true,
            message: '单击'+JSON.stringify(row),
            type: 'success',
          });
        }
    }
}
</script>
```

行双击方法
----------------------------------------------------------------------------------------------
双击一行数据时回调`row-dblclick`方法，同时返回当前行的`row`数据，`event`当前的操作对象，`column`当前列的属性

```vue
<avue-crud :data="data" :option="option" @row-dblclick="handleRowDBLClick"></avue-crud>

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
          column:[
             {
              label:'姓名',
              prop:'name'
            }, {
              label:'性别',
              prop:'sex'
            }
          ]
        }
      }
    },
    methods: {
       handleRowDBLClick (row, event) {
        this.$notify({
          showClose: true,
          message: '双击'+JSON.stringify(row),
          type: 'success',
        });
      }
    }
}
</script>
```

行拖拽排序
----------------------------------------------------------------------------------------------
Tips 2.9.0+

```html
<!-- 导入需要的包 （一定要放到index.html中的head标签里） -->
<script src="https://cdn.staticfile.net/Sortable/1.10.0-rc2/Sortable.min.js"></script>
```

`rowSort`设置为`true`即可开启拖拽功能，`sortable-change`为拖拽后的回调方法

```vue
<avue-crud :option="option" :data="data" @sortable-change="sortableChange"></avue-crud>

<script>
export default {
  data(){
    return {
       data:[
          {
            text1:'内容1-1',
            text2:'内容1-2'
         },{
            text1:'内容2-1',
            text2:'内容2-2'
         },{
            text1:'内容3-1',
            text2:'内容3-2'
         },{
            text1:'内容4-1',
            text2:'内容4-2'
         },{
            text1:'内容5-1',
            text2:'内容5-2'
         }
       ],
       option:{
          rowSort:true,
          column: [{
            label: '列内容1',
            prop: 'text1',
          }, {
            label: '列内容2',
            prop: 'text2',
          }]
       }
    }
  },
  methods:{
     sortableChange(oldindex, newindex) {
        this.$message.success(oldindex+','+newindex)
        console.log(oldindex, newindex)

      }
  }
}
</script>
```

行合并
--------------------------------------------------------------------------
Tips

如果数据不确定参考[动态数据行和列合并](https://v2.avuejs.com/crud/crud-rc.html)

通过给传入`spanMethod`方法可以实现合并行或列，方法的参数是一个对象，里面包含当前行`row`、当前列`column`、当前行号`rowIndex`、当前列号`columnIndex`四个属性。该函数可以返回一个包含两个元素的数组，第一个元素代表`rowspan`，第二个元素代表`colspan`。也可以返回一个键名为`rowspan`和`colspan`的对象。

```vue
<avue-crud
  :data="data"
  :option="option"
  :span-method="spanMethod"
></avue-crud>

<script>
  export default {
    data() {
      return {
        data: [
          {
            id: '12987122',
            name: '王小虎',
            amount1: '234',
            amount2: '3.2',
            amount3: 10
          },
          {
            id: '12987123',
            name: '王小虎',
            amount1: '165',
            amount2: '4.43',
            amount3: 12
          },
          {
            id: '12987124',
            name: '王小虎',
            amount1: '324',
            amount2: '1.9',
            amount3: 9
          },
          {
            id: '12987125',
            name: '王小虎',
            amount1: '621',
            amount2: '2.2',
            amount3: 17
          },
          {
            id: '12987126',
            name: '王小虎',
            amount1: '539',
            amount2: '4.1',
            amount3: 15
          }
        ],
        option: {
          border: true,
          menu:false,
          column: [
            {
              label: 'ID',
              prop: 'id'
            },
            {
              label: '姓名',
              prop: 'name'
            },
            {
              label: '数值 1',
              prop: 'amount1'
            },
            {
              label: '数值 2',
              prop: 'amount2'
            },
            {
              label: '数值 3',
              prop: 'amount3'
            }
          ]
        }
      }
    },
    methods: {
      spanMethod({ row, column, rowIndex, columnIndex }) {
        if (rowIndex % 2 === 0) {
          if (columnIndex === 0) {
            return [1, 2]
          } else if (columnIndex === 1) {
            return [0, 0]
          }
        }
      }
    }
  }
</script>
```

[表头配置](https://v2.avuejs.com/crud/crud-head/) [表格列配置项](https://v2.avuejs.com/crud/crud-column/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号