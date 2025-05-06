inputTabel表格选择器
===============

值:0  
格式化值:0  
值:[0, 1]  

```vue
<el-row :span="24">
  <el-col :span="6">
    值:{{form}}<br/>
    <avue-input-table :props="props" :children="children" :on-load="onLoad" v-model="form" placeholder="请选择数据"></avue-input-table>
    格式化值:{{form}}<br/>
    <avue-input-table :props="props" :children="children" :formatter="formatter" :on-load="onLoad" v-model="form" placeholder="请选择数据"></avue-input-table>
    值:{{form1}}<br/>
    <avue-input-table multiple :props="props" :children="children" :formatter="formatter1" :on-load="onLoad1" v-model="form1" placeholder="请选择数据"></avue-input-table>
  </el-col>
</el-row>

<script>
export default {
  data() {
    return {
      children: {
        border: true,
        column: [
          {
            label: '姓名',
            width: 120,
            search: true,
            prop: 'name'
          },
          {
            label: '性别',
            search: true,
            prop: 'sex'
          }
        ]
      },
      props: {
        label: 'name',
        value: 'id'
      },
      form: '0',
      form1: [0,1]
    }
  },
  methods: {
    formatter1(row) {
      if (Array.isArray(row)) {
        return row.map(ele => ele.name + '格式化').join(',')
      } else {
        return row.name + '格式化'
      }
    },
    onLoad1({ page, value, data }, callback) {
      if (value) {
        this.$message.success('首次查询' + value)
        callback([
          {
            id: '0',
            name: '张三',
            sex: '男',
            age: 18
          },
          {
            id: '2',
            name: '王五',
            sex: '女'
          }
        ])
        return
      }
      if (data) {
        this.$message.success('搜索查询参数' + JSON.stringify(data))
      }
      if (page) {
        this.$message.success('分页参数' + JSON.stringify(page))
      }
      callback({
        total: 2,
        data: [
          {
            id: '0',
            name: '张三',
            sex: '男',
            age: 18
          },
          {
            id: '1',
            name: '李四',
            sex: '女',
            disabled: true,
            age: 18
          },
          {
            id: '2',
            name: '王五',
            sex: '女'
          }
        ]
      })
    },
    formatter(row) {
      if (!row.name) return ''
      return row.name + '-' + row.sex
    },
    onLoad({ page, value, data }, callback) {
      if (value) {
        this.$message.success('首次查询' + value)
        callback({
          id: '0',
          name: '张三',
          sex: '男'
        })
        return
      }
      if (data) {
        this.$message.success('搜索查询参数' + JSON.stringify(data))
      }
      if (page) {
        this.$message.success('分页参数' + JSON.stringify(page))
      }
      callback({
        total: 2,
        data: [
          {
            id: '0',
            name: '张三',
            sex: '男'
          },
          {
            id: '1',
            name: '李四',
            sex: '女'
          }
        ]
      })
    }
  }
}
</script>
```

[inputMap地图选择器](https://v2.avuejs.com/component/input-map/) [array 数组输入框](https://v2.avuejs.com/component/array/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号