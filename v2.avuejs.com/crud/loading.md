等待加载
====

普通用法
----------------------------------------------------------------------------------------

加载等待框  
`table-loading`属性可以配置等待加载状态

```vue
<el-button type="primary" icon="el-icon-sort" @click="getOption">加载等待框</el-button>
<br /> <br />
<avue-crud :key="reload" :data="data" :option="option" :table-loading="loading"></avue-crud>

<script>
export default {
  data () {
    return {
      reload: Math.random(),
      loading: true,
      data: [],
      option: {
        border: true,
        align: 'center',
        menuAlign: 'center',
        loadingText: "Loading...",
        loadingSpinner: "svg",
        loadingSvgViewBox: "-10, -10, 50, 50",
        loadingBackground: "rgba(122, 122, 122, 0.8)",
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
    };
  },
  created () {
    this.getOption()
  },
  methods: {
    getOption () {
      this.loading = true;
      this.$message.success('模拟2s后服务端动态加载');
      setTimeout(() => {
        this.data = [
          {
            name: '张三',
            sex: '男',
            province: '110000'
          },
          {
            name: '李四',
            sex: '女',
            province: '120000'
          }
        ]
        this.loading = false;
        this.reload = Math.random()
      }, 2000)
    }
  }
}
</script>
```

[空状态](https://v2.avuejs.com/crud/crud-empty/) [拖拽排序](https://v2.avuejs.com/crud/crud-sortable/)


您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本，关注Avue Cloud公众号