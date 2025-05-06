array 数组输入框
===========

值:["第一条", "第二条", "第三条", "第四条"]

```vue
<el-row :span="24">
  <el-col :span="6">
    值:{{form}}<br />
    <avue-array v-model="form" placeholder="请输入内容"></avue-array>
  </el-col>
</el-row>
<script>
export default {
  data() {
    return {
      form: ['第一条', '第二条', '第三条', '第四条'],
    }
  },
}
</script>
```

[inputTabel表格选择器](https://v2.avuejs.com/component/input-table/) [img图片输入框](https://v2.avuejs.com/component/img/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号