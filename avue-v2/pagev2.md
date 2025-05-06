整理后的 Markdown 内容，去除了多余的行号数据：

---

# 分页

---

## 页码和条数

页码:1 页码+1  
条数:10 条数+10  
总数:1000 总页数+10

`currentPage`当前页码，`total`总条数，`pageSize`每页多少条数据

```vue
<p>
  页码:{{page.currentPage}}
  <el-button type="primary" @click="page.currentPage=page.currentPage+1">页码+1</el-button>
</p>
<p>
  条数:{{page.pageSize}}
  <el-button type="primary" @click="page.pageSize=page.pageSize+10">条数+10</el-button>
</p>
<p>
  总数:{{page.total}}
  <el-button type="primary" @click="page.total=page.total+10">总页数+10</el-button>
</p>
<avue-crud :data="data" :option="option" :page.sync="page"></avue-crud>

<script>
export default {
  data() {
    return {
      page:{ 
        total: 1000, 
        currentPage: 1, 
        pageSize: 10
      },
      data: [],
      option: {
        header:false,
        column:[
          {
            label:'姓名',
            prop:'name'
          }
        ]
      }
    }
  }
}
</script>
```

---

## 设置最大页码按钮数

`pagerCount`属性默认为7

```vue
<avue-crud :data="data" :option="option" :page.sync="page"></avue-crud>

<script>
export default {
  data() {
    return {
      page:{
        pagerCount:11,
        total:1000
      },
      data: [],
      option: {
        header:false,
        column:[
          {
            label:'姓名',
            prop:'name'
          }
        ]
      }
    }
  }
}
</script>
```

---

## 无背景色的分页

`background`属性默认为`true`

```vue
<avue-crud :data="data" :option="option" :page.sync="page"></avue-crud>

<script>
export default {
  data() {
    return {
      page:{
        background:false,
        total:1000
      },
      data: [],
      option: {
        header:false,
        column:[
          {
            label:'姓名',
            prop:'name'
          }
        ]
      }
    }
  }
}
</script>
```

---

## 附加功能

简单模式 复杂模式

`layout`属性中的每一项都是附加功能，可以自行操作

```vue
<el-button type="small" @click="page.layout='sizes,pager'">简单模式</el-button>
<el-button type="small" @click="page.layout='total, sizes, prev, pager, next, jumper'">复杂模式</el-button>
<avue-crud :data="data" :option="option" :page.sync="page"></avue-crud>

<script>
export default {
  data() {
    return {
      page:{
        total:1000,
        layout: "total, sizes, prev, pager, next, jumper", 
      },
      data: [],
      option: {
        header:false,
        column:[
          {
            label:'姓名',
            prop:'name'
          }
        ]
      }
    }
  }
}
</script>
```

---

## 综合用法

Tips:

- 配合[增删改查方法去使用](https://v2.avuejs.com/crud/crud-fun.html)实现完整的表格功能  
- `{ "pageSize": 20, "pagerCount": 5 }`

首次加载调用`on-load`方法加载数据，返回`page`分页对象信息,赋值`page`的`total`总条数即可。如果`total`为0，或者`simplePage`为`true`且只有1页的时候，分页选择器会隐藏。

```vue
{{page}}
<avue-crud
  :data="data"
  :option="option"
  :page.sync="page"
  @on-load="onLoad"
></avue-crud>

<script>
export default {
  data() {
    return {
      page: {
        pageSize: 20,
        pagerCount:5
      },
      data: [],
      option: {
        align: 'center',
        menuAlign: 'center',
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
  methods: {
    onLoad(page) {
      this.$message.success('分页信息:' + JSON.stringify(page))
      this.page.total = 40
      // 模拟分页
      if (this.page.currentPage === 1) {
        this.data = [
          {
            id:1,
            name: '张三',
            sex: '男'
          },
          {
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
          },
          {
            id:4,
            name: '赵六',
            sex: '女'
          }
        ]
      }
    }
  }
}
</script>
```

---

## 自定义分页

```json
{ "currentPage": 1, "total": 40, "layout": "total,pager,prev, next", "background": false, "pageSize": 10 }
```

实际的用法要后台配置，将后台返回值赋值给 `page` 中的属性。`page` 是分页对象注入，`total`为总页数，`pageSizes`为分页信息，`currentPage`为当前第几页，`pageSize`每一页加载多少条数据。

点击页码会调用`current-change`方法回调当前页数，点击每页多少条则会调用`size-change`方法回调。

```vue
{{page}}
<avue-crud
  :data="data"
  :option="option"
  :page.sync="page"
  @size-change="sizeChange"
  @current-change="currentChange"
></avue-crud>

<script>
export default {
  data() {
    return {
      page: {
        currentPage: 1,
        total: 0,
        layout: "total,pager,prev, next",
        background: false,
        pageSize: 10
      },
      data: [],
      option: {
        align: 'center',
        menuAlign: 'center',
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
  created() {
    this.getList()
  },
  methods: {
    getList() {
      this.page.total = 40
      if (this.page.currentPage === 1) {
        this.data = [
          {
            id:1,
            name: '张三',
            sex: '男'
          },
          {
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
          },
          {
            id:4,
            name: '赵六',
            sex: '女'
          }
        ]
      }
    },
    sizeChange(val) {
      this.page.currentPage = 1
      this.page.pageSize = val
      this.getList()
      this.$message.success('行数' + val)
    },
    currentChange(val) {
      this.page.currentPage = val
      this.getList()
      this.$message.success('页码' + val)
    }
  }
}
</script>
```

---

[Object对象形式](https://v2.avuejs.com/crud/crud-object/) | [搜索](https://v2.avuejs.com/crud/crud-search/)

---

### 说明

您正在浏览基于 Vue 2.x 的 Avue 文档；**[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本。

关注 Avue Cloud 公众号。

---

如需进一步调整或需求，欢迎告知！