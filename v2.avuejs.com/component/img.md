img图片输入框
========

值: ["https://avuejs.com/images/logo-bg.jpg", "https://avuejs.com/images/logo-bg.jpg"]

```vue
<el-row :span="24">
  <el-col :span="6">
     值:{{form}}<br/>
    <avue-array type="img" v-model="form" placeholder="请输入内容" ></avue-array>
  </el-col>
</el-row>

<script>
export default {
    data() {
      return {
        form:[
          'https://avuejs.com/images/logo-bg.jpg',
          'https://avuejs.com/images/logo-bg.jpg',
        ]
      }
    }
}
</script>
```

[array 数组输入框](https://v2.avuejs.com/component/array/) [url超链接输入框](https://v2.avuejs.com/component/url/)

您正在浏览基于 Vue 2.x 的 Avue 文档; **[点击这里](https://avuejs.com/)** 查看 Vue 3.x 的升级版本

关注Avue Cloud公众号