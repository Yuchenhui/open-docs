表格树
===

Tips  
* 配置rowKey主键(默认为id)  
* 配置rowParentKey父类主键(默认为parentId)  

普通用法  
-------------------------------------------------------------------------------------

`defaultExpandAll`属性是否全部展开,其他用法和普通crud一致,一定要配置`rowKey`主键和`rowParentKey`父类主键，如果非懒加载树形不显示，删除据中`hasChildren`字段

```vue
<avue-crud v-model="form" :option="option" :data="data" ref="crud" @row-save="rowSave" @row-update="rowUpdate" @row-del="rowDel">
  <template slot="icon" slot-scope="scope">
    <i :class="scope.row.icon" style="font-size:24px"></i>
  </template>
  <template slot="menu" slot-scope="{row,size,type}">
    <el-button :size="size" :type="type" @click="handleAdd(row)">新增子级</el-button>
  </template>
</avue-crud>
<script>
export default {
  data(){
    return {
      parentId: undefined,
      form: {},
      data: [
        {
          id: 10,
          event: '事件1',
          timeLine: 50,
          comment: '无'
        },
        {
          id: 1,
          event: '事件1',
          timeLine: 100,
          comment: '无',
          children: [
            {
              parentId: 1,
              id: 2,
              event: '事件2',
              timeLine: 10,
              comment: '无'
            },
            {
              parentId: 1,
              id: 3,
              event: '事件3',
              timeLine: 90,
              comment: '无',
              children: [
                {
                  parentId: 3,
                  id: 4,
                  event: '事件4',
                  timeLine: 5,
                  comment: '无'
                },
                {
                  parentId: 3,
                  id: 5,
                  event: '事件5',
                  timeLine: 10,
                  comment: '无'
                }
              ]
            }
          ]
        }
      ],
      option: {
        headerAlign: 'center',
        align: 'center',
        border: true,
        index: true,
        rowKey: 'id',
        rowParentKey: 'parentId',
        // defaultExpandAll:true,
        column: [
          {
            label: '事件',
            prop: 'event',
            align: 'left',
            width: 200
          },
          {
            label: '时间线',
            prop: 'timeLine'
          },
          {
            label: '备注',
            prop: 'comment'
          }
        ]
      }
    }
  },
  methods: {
    rowDel(row, index, done){
      done(row)
    },
    rowSave(row, done){
      row.parentId = this.parentId;
      row.id = new Date().getTime();
      this.parentId = undefined;
      done(row)
    },
    rowUpdate(row, index, done){
      done(row)
    },
    handleAdd(row){
      this.parentId = row.id;
      this.$refs.crud.rowAdd();
    }
  }
}
</script>
```

表格树懒加载  
---------------------------------------------------------------------------------------------------------

`lazy`为`true`,同时接受`tree-load`函数的回调即可，通过指定`row`中的`hasChildren`字段来指定哪些行是包含子节点

```vue
<avue-crud ref="crud" :option="option1" :data="data1" @tree-load="treeLoad" @row-save="rowSave" @row-update="rowUpdate">
  <template slot="menu" slot-scope="{row,size,type}">
    <el-button :size="size" :type="type" @click="handleAdd(row)">新增子级</el-button>
  </template>
</avue-crud>
<script>
export default {
  data(){
    return {
      parentId: undefined,
      option1: {
        lazy: true,
        rowKey: 'id',
        column: [
          {
            label: '姓名',
            prop: 'name'
          },
          {
            label: '日期',
            prop: 'date'
          },
          {
            label: '地址',
            prop: 'address',
            overHidden: true
          }
        ]
      },
      data1: [
        {
          id: 1,
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },
        {
          id: 2,
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1517 弄'
        },
        {
          id: 3,
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1519 弄',
          hasChildren: true
        },
        {
          id: 4,
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }
      ]
    }
  },
  methods: {
    rowDel(row, index, done){
      done(row)
    },
    rowSave(row, done){
      row.parentId = this.parentId;
      row.id = new Date().getTime();
      this.parentId = undefined;
      done(row)
    },
    rowUpdate(row, index, done){
      done(row)
    },
    handleAdd(row){
      this.parentId = row.id;
      this.$refs.crud.rowAdd();
    },
    treeLoad(tree, treeNode, resolve) {
      setTimeout(() => {
        resolve([
          {
            id: new Date().getTime(),
            date: '2016-05-01',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1519 弄',
            hasChildren: true
          }
        ]);
      }, 1000);
    }
  }
}
</script>
```

左树右表  
-------------------------------------------------------------------------------------

这是`tree`组件和`crud`组件的结合使用，主要是用`nodeClick`回调刷新`crud`数据

```vue
<el-container>
  <el-aside width="200px">
    <avue-tree :option="treeOption" :data="treeData" @node-click="nodeClick"></avue-tree>
  </el-aside>
  <el-main>
    <avue-crud
      :data="loadData"
      :option="loadOption"
      v-model="obj"
    ></avue-crud>
  </el-main>
</el-container>

<script>
export default {
  data() {
    return {
      obj: {},
      treeData: [
        {
          value: 0,
          label: '一级部门',
          children: [
            {
              value: 1,
              label: '一级部门1'
            }
          ]
        }
      ],
      treeOption: {
        defaultExpandAll: true,
        formOption: {
          labelWidth: 100,
          column: [
            {
              label: '自定义项',
              prop: 'test'
            }
          ]
        },
        props: {
          labelText: '标题',
          label: 'label',
          value: 'value',
          children: 'children'
        }
      },
      loadData: [],
      loadData1: [
        {
          name: '张三',
          sex: '男'
        }
      ],
      loadData2: [
        {
          name: '李四2',
          sex: '女'
        }
      ],
      loadOption: {
        column: [
          {
            label: '姓名',
            prop: 'name'
          },
          {
            label: '性别',
            prop: 'sex'
          }
        ]
      }
    }
  },
  created(){
    this.loadData = this.loadData1;
  },
  methods: {
    nodeClick(data){
      if(data.value == 0){
        this.loadData = this.loadData1;
      } else if(data.value == 1){
        this.loadData = this.loadData2;
      }
      this.$message.success(JSON.stringify(data))
    }
  }
}
</script>
```

[导入导出](https://v2.avuejs.com/crud/crud-export/) [父子表](https://v2.avuejs.com/crud/crud-children/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号