表头配置
====

固定表头
-------------------------------------------------------------------------------------

设置`height`时当表格的高度超过设定值，就会出现滚动条，从而达到固定表头的效果

```vue
<avue-crud :data="data" :option="option" ></avue-crud>

<script>
export default {
    data() {
      return {
        data: [
          { name:'张三', sex:'男' }, 
          { name:'李四', sex:'女' },
          { name:'张三', sex:'男' }, 
          { name:'李四', sex:'女' },
          { name:'张三', sex:'男' }, 
          { name:'李四', sex:'女' },
          { name:'张三', sex:'男' }, 
          { name:'李四', sex:'女' }
        ],
        option:{
          height:300,
          column:[
             {
              label:'姓名',
              prop:'name',
              width:200,
              fixed:true
            }, {
              label:'性别',
              width:300,
              prop:'sex'
            }, {
              label:'日期',
              width:300,
              prop:'datetime'
            }, {
              label:'地址',
              width:300,
              prop:'address'
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

隐藏表头
-------------------------------------------------------------------------------------

设`showHeader`属性为`false`即可隐藏表头

```vue
<avue-crud :data="data" :option="option" ></avue-crud>

<script>
export default {
    data() {
      return {
        data: [
          { name:'张三', sex:'男' }, 
          { name:'李四', sex:'女' }
        ],
        option:{
          showHeader:false,
          column:[
             {
              label:'姓名',
              prop:'name',
              width:200,
              fixed:true
            }, {
              label:'性别',
              width:300,
              prop:'sex'
            }, {
              label:'日期',
              width:300,
              prop:'datetime'
            }, {
              label:'地址',
              width:300,
              prop:'address'
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

自定义表头样式
-------------------------------------------------------------------------------------------------------------------

```css
.warning-row {
 background-color: #F56C6C !important;
 color:#fff;
}
.success-row {
 background-color: #67C23A !important;
 color:#fff;
}
```

可以通过指定组件的 `header-class-name`

```vue
<avue-crud :data="data" :option="option" :header-cell-class-name="headerCellClassName"
             :header-row-class-name="headerRowClassName" ></avue-crud>

<script>
export default {
    data() {
      return {
        data: [
          { name:'张三', sex:'男' }, 
          { name:'李四', sex:'女' }
        ],
        option:{
          column:[
             { label:'姓名', prop:'name' },
             { label:'性别', prop:'sex' }
          ]
        },
      };
    },
    methods: {
       headerRowClassName ({ rowIndex }) {
        console.log({ rowIndex })
      },
      headerCellClassName ({ column, columnIndex, row, rowIndex }) {
        if (columnIndex == 0) {
          return 'warning-row'
        } else if (columnIndex == 1) {
          return 'success-row'
        }
      } 
    }
}
</script>
```

表头单元格样式
-------------------------------------------------------------------------------------------------------------------

开放了`header-cell-style`和`header-row-style`方法

```vue
<avue-crud :data="data" :option="option"  :header-row-style="headerRowStyle"
             :header-cell-style="headerCellStyle" ></avue-crud>

<script>
export default {
    data() {
      return {
        data: [
          { name:'张三', sex:'男' }, 
          { name:'李四', sex:'女' }
        ],
        option:{
          column:[
             { label:'姓名', prop:'name' },
             { label:'性别', prop:'sex' }
          ]
        },
      };
    },
    methods: {
       headerRowStyle ({ rowIndex }) {
          console.log({ rowIndex })
        },
        headerCellStyle ({ column, columnIndex, row, rowIndex }) {
          if (columnIndex == 0) {
            return {
              color: 'green',
              fontWeight: 'bold',
              fontSize: '20'
            }
          } else {
            return {
              color: 'red',
              fontWeight: 'bold',
              fontSize: '20'
            }
          }
        }
    }
}
</script>
```

多级表头
-------------------------------------------------------------------------------------

只要在配置中添加children层级嵌套即可

```vue
<avue-crud :option="option" :data="data" ></avue-crud>
<script>
export default {
    data() {
      return {
        option: {
          excelBtn:true,
          border: true,
          index: true,
          expandLevel: 3,
          headerAlign: 'center',
          align: 'center',
          tree: true,
          labelWidth: 100,
          column: [
            {
              label: '姓名',
              prop: 'name',
              width:140,
            }, {
              label: '性别1',
              prop: 'sex',
            }, {
              label: '自定义图标',
              prop: 'icon',
              type: "icon",
              iconList: [{
                label: '基本图表',
                list: ['el-icon-time', 'el-icon-bell', 'el-icon-star-on']
              }]
            }, {
              label: '多级表头',
              children: [{
                label: '信息',
                children: [{
                  label: '年龄',
                  prop: 'age'
                }, {
                  label: '手机号',
                  prop: 'phone',
                }]
              }, {
                label: '地区',
                prop: 'address',
                type: 'select',
                props: {
                    label: 'name',
                    value: 'code'
                },
                dicUrl:'https://cli.avuejs.com/api/area/getProvince'
              }]
            }, {
              label: '测试',
              prop: 'test',
            }, {
              label: '手机信息1',
              prop: 'phone1'
            }]
        },
        data: [{
          name: '张三',
          age: 14,
          address: '110000',
          phone1: '17547400800',
          phone: '17547400800',
          icon: 'el-icon-time',
          test: 1,
          sex: '男'
        }, {
          name: '王五',
          age: 10,
          address: '120000',
          test: 1,
          sex: '女',
          icon: 'el-icon-star-on',
          phone1: '17547400800',
          phone: '17547400800'
        }]
      }
    }
}
</script>
```

自定义列表头
---------------------------------------------------------------------------------------------------------

设置列的属性`headerslot`为`true`，在卡槽中指定列的`prop`加上`Header`作为卡槽的名称

```vue
<avue-crud ref="crud" :option="option" :data="data">
  <template slot="nameHeader" slot-scope="{column}">
      <el-tag>{{(column || {}).label}}-{{(column || {}).prop}}</el-tag>
  </template>
</avue-crud>
<script>
export default {
    data() {
      return {
        option: {
          column: [
            { label: '姓名', prop: 'name', headerslot:true },
            { label: '年龄', prop: 'sex' }
          ]
        },
        data: [
          { name:'张三', sex:'男' },
          { name:'李四', sex:'女' }
        ],
      }
    }
}
</script>
```

自定义菜单栏左边
-----------------------------------------------------------------------------------------------------------------------------

卡槽为`menuLeft`为表格菜单左边的位置

```vue
<avue-crud :data="data" :option="option">
  <template slot="menuLeft" slot-scope="{size}">
    <el-button type="primary" :size="size">自定义按钮</el-button>
  </template>
</avue-crud>

<script>
export default {
    data() {
      return {
        data: [
          { name:'张三', sex:'男' },
          { name:'李四', sex:'女' }
        ],
        option:{
          column:[
             { label:'姓名', prop:'name' },
             { label:'性别', prop:'sex' }
          ]
        },
      };
    }
}
</script>
```

自定义菜单栏右边
-----------------------------------------------------------------------------------------------------------------------------

卡槽为`menuRight`为表格菜单右边的位置

```vue
<avue-crud :data="data" :option="option">
  <template slot="menuRight" slot-scope="{size}">
     <el-button type="primary" icon="el-icon-edit" circle :size="size"></el-button>
  </template>
</avue-crud>

<script>
export default {
    data() {
      return {
        data: [
          { name:'张三', sex:'男' },
          { name:'李四', sex:'女' }
        ],
        option:{
          column:[
             { label:'姓名', prop:'name' },
             { label:'性别', prop:'sex' }
          ]
        },
      };
    }
}
</script>
```